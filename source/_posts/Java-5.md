---
title: Spring Boot AWS S3 연결 및 사용법
subtitle: '업로드, 다운로드, 버킷 리스트, 파일 URL'
catalog: true
tags:
  - Java
  - Spring Boot
  - AWS
  - S3
catagories:
  - Java
  - Spring Boot
  - AWS
  - S3
comments: true
date: 2018-07-27 16:26:15
header-img:
---


## # 글의 목적

> Spring Boot에서 AWS S3 Bucket과 연결하여 이미지 파일의 이름을 가져오고 파일을 업로드하고 다운로드 하는 방법에 대해서 정리하고자 합니다. 실무에서 S3에 새로운 이미지파일 (예를 들어, 아이콘)을 올리면 앱에 바로 반영되게끔 하고자 구현하게 되었습니다.

## # 환경 구성

* AWS 계정과 S3 Bucket이 이미 생성되었다는 가정하에 시작합니다. 

> 아래는 샘플 이미지가 추가된 Bucket의 모습입니다.

![screen shot 2018-07-27 at 3 46 26 pm](https://user-images.githubusercontent.com/34642220/43305890-52141c48-91b4-11e8-9ef4-13dccb783089.png)

#### # gradle 또는 maven 에 의존성 추가

저는 maven 을 사용중이기 때문에 아래와 의존성을 추가 하였습니다.

[Maven Central Link](https://search.maven.org/#search%7Cga%7C1%7Caws%20java%20sdk)에서 최신 버전을 확인 할 수 있습니다.

```
<!-- aws-java-sdk -->
<dependency>
    <groupId>com.amazonaws</groupId>
    <artifactId>aws-java-sdk</artifactId>
    <version>1.11.106</version>
</dependency>
```


#### # IAM 정책에서 ACCESS_KEY 와 SECRET_KEY 확인

![screen shot 2018-07-27 at 3 57 09 pm](https://user-images.githubusercontent.com/34642220/43306498-5b0c1cd6-91b6-11e8-8196-71bc2601c510.png)

<font color="red"> 사용자에 S3 Access 권한이 있어야 합니다. 권한이 없을 경우, Users > Permission Tab 에서 추가해주세요. </font>

## # 예제

#### # AmazonS3Util.java

<pre>
<code>
  private static Logger logger = LoggerFactory.getLogger(AmazonS3Util.class);

  private static final String accessKey = "YOUR ACCESS_KEY";
  private static final String secretKey = "YOUR SECRET_KEY";
  private static final String region = "YOUR REGION";
  private static final String bucketName = "YOUR BUCKET NAME";

  private static AmazonS3 s3client() {
    BasicAWSCredentials awsCredentials = new BasicAWSCredentials(accessKey, secretKey);
    AmazonS3 s3Client = AmazonS3ClientBuilder.standard().withRegion(Regions.fromName(region))
        .withCredentials(new AWSStaticCredentialsProvider(awsCredentials)).build();
    return s3Client;
  }

  // 업로드
  public static void uploadFile(String fileName, String uploadFilePath) {
    try {
      File file = new File(uploadFilePath);
      s3client().putObject(new PutObjectRequest(bucketName, fileName, file));
      System.out.println("================== Upload File - Done! ==================");
    } catch (AmazonServiceException ase) {
      logger.info("Caught an AmazonServiceException from PUT requests, rejected reasons:");
      logger.info("Error Message:    " + ase.getMessage());
      logger.info("HTTP Status Code: " + ase.getStatusCode());
      logger.info("AWS Error Code:   " + ase.getErrorCode());
      logger.info("Error Type:       " + ase.getErrorType());
      logger.info("Request ID:       " + ase.getRequestId());
    } catch (AmazonClientException ace) {
      logger.info("Caught an AmazonClientException: ");
      logger.info("Error Message: " + ace.getMessage());
    }
  }

  // 다운로드 
  public static void downloadFile(String keyName) {
    try {
      System.out.println("Downloading an object");
      S3Object s3object = s3client().getObject(new GetObjectRequest(bucketName, keyName));
      System.out.println("Content-Type: " + s3object.getObjectMetadata().getContentType());
      // .txt 파일이면 파일 읽는 부분
      displayText(s3object.getObjectContent());
      logger.info("================== Downloade File - Done! ==================");
    } catch (AmazonServiceException ase) {
      logger.info("Caught an AmazonServiceException from GET requests, rejected reasons:");
      logger.info("Error Message:    " + ase.getMessage());
      logger.info("HTTP Status Code: " + ase.getStatusCode());
      logger.info("AWS Error Code:   " + ase.getErrorCode());
      logger.info("Error Type:       " + ase.getErrorType());

    } catch (AmazonClientException ace) {
      logger.info("Caught an AmazonClientException: ");
      logger.info("Error Message: " + ace.getMessage());
    }
  }

  // .txt 파일 읽어드리는 함수
  private static void displayText(InputStream input) {
    BufferedReader reader = new BufferedReader(new InputStreamReader(input));
    while (true) {
      String line = null;
      try {
        line = reader.readLine();
      } catch (IOException e) {
        e.printStackTrace();
      }
      if (line == null)
        break;
      System.out.println(line);
    }
  }

  // 특정 버켓에 들어있는 파일 리스트 가져오기
  public static List<String> getObjectsListFromFolder() {

    ListObjectsRequest listObjectsRequest = new ListObjectsRequest().withBucketName(bucketName);

    List<String> fileNames = new ArrayList<>();

    ObjectListing objects = s3client().listObjects(listObjectsRequest);
    for (;;) {
      List<S3ObjectSummary> summaries = objects.getObjectSummaries();
      if (summaries.size() < 1) {
        break;
      }
      summaries.forEach(s -> fileNames.add(s.getKey()));
      objects = s3client().listNextBatchOfObjects(objects);
    }
    return fileNames;
  }

  // 파일 URL 가져오기
  public static String getFileURL(String fileName) {
    String imageName = (fileName).replace(File.separatorChar, '/');
    String imageUrl = s3client()
        .generatePresignedUrl(new GeneratePresignedUrlRequest(bucketName, imageName)).toString();
    return imageUrl;
  }
</pre>
</code>

## # 마무리

>구글링을 해보면 인터넷에 나와있는 사용법이 많이 있지만 대부분 업로드와 다운로드 뿐이였습니다.
특정 버킷의 파일리스트를 가져오고 그 파일들의 URL을 알 수 있는 함수가 필요하여 영어로 된 자료에서 참고하여
저희 회사 시스템에 맞게끔 구현하였습니다.

>궁금하신 부분이 있으면 언제든지 댓글로 남겨주세요 ^^
잘못된 부분이나 오타도 언제든 환영합니다.




