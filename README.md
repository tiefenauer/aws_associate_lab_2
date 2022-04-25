# Lab 2
- Step 9: updated `config.properties` with the region and bucket name

edited `createBucket.java`
- Step 12: by adding an `S3Client` instance with the correct rgion
```java
S3Client s3 = S3Client.builder()
      .region(labRegion)
      .build();
```
- Step 13: by creating a `HeadBucketRequest` to check if the bucket exists
```java
   HeadBucketRequest request = HeadBucketRequest.builder()
         .bucket(bucketName)
         .build();
```
- Step 15: Created a `S3Waiter` instance to create an S3 bucket asynchronously:
```java
   S3Waiter s3Waiter = s3Client.waiter(); 
```
- Step 16: Created a `CreateBucketRequest` instance to create a bucket:
```java
CreateBucketRequest bucketRequest = CreateBucketRequest.builder()
      .bucket(bucketName)
      .build();
```
- Step 18: recombiled class and executed it using Mavn:
```
$ mvn -q exec:java -Dexec.mainClass="dev.labs.s3.createBucket"
```

edited `uploadObject.java`:
- Step 20: created metadata hashmap with custom metadata:
```java
      Map<String, String> metadata = new HashMap<>();
      metadata.put("x-amz-meta-myVal2", "lab2-testing-upload");
```
- Step 21: created `PutObjectRequest` instance to add metadata to every uploaded object like the CSV:
```java
   PutObjectRequest putObject = PutObjectRequest.builder()
         .bucket(bucketName)
         .key(objectKey)
         .metadata(metadata)
         .build();
```
- Step 23: recompiled the class and executed it to upload the CSV:
```
$ mvn -q exec:java -Dexec.mainClass="dev.labs.s3.uploadObject"
```

edited `processObject.java`:
- Step 25/TODO 7: Created a `GetObjectRequest` instance to download the CSV
```java
            GetObjectRequest getObjectRequest = GetObjectRequest.builder()
                    .bucket(bucketName)
                    .key(objectKey)
                    .build();
```
- Step 27: uploaded the `notes.json` to the bucked
```java
                s3.putObject(putObject,
                        RequestBody.fromFile(Paths.get(objectNewKey)));
```
- Step 29: recompiled and executed the class to upload the notes.json file:
```
$ mvn -q exec:java -Dexec.mainClass="dev.labs.s3.processObject"
```

To read up:
- S3 Object metadata
- S3 in general