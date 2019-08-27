# curlToArtifactory

```bash
docker run -p 8086:8081 docker.bintray.io/jfrog/artifactory-oss
```
# curl cli
```bash
APIKEY=AKCp5dL3KyFzU4mULLu18Z8YhaaCV6hgAHSnGfxDKp2qNsnZMfFCPb8C49EXCzeXuPgnBTHwk
FILE=example.jar
ARTIFACT_MD5_CHECKSUM=$(md5sum $FILE | awk '{print $1}')
ARTIFACT_SHA1_CHECKSUM=$(shasum -a 1 $FILE | awk '{ print $1 }')
curl --upload-file "$FILE" \
--header "X-Checksum-MD5:${ARTIFACT_MD5_CHECKSUM}" \
--header "X-Checksum-Sha1:${ARTIFACT_SHA1_CHECKSUM}" \
-u "admin:$APIKEY" \
-v http://localhost:8086/artifactory/libs-release-local/
```

## response 
```bash
*   Trying ::1:8086...
* TCP_NODELAY set
* Connected to localhost (::1) port 8086 (#0)
* Server auth using Basic with user 'admin'
> PUT /artifactory/libs-release-local/example.jar HTTP/1.1
> Host: localhost:8086
> Authorization: Basic YWRtaW46QUtDcDVkTDNLeUZ6VTRtVUxMdTE4WjhZaGFhQ1Y2aGdBSFNuR2Z4REtwMnFOc25aTWZGQ1BiOEM0OUVYQ3plWHVQZ25CVEh3aw==
> User-Agent: curl/7.65.3
> Accept: */*
> X-Checksum-MD5:b31fd78f3fe6f41521dea5bd08df06bc
> X-Checksum-Sha1:3310293b545f32644aa55a4509d8b3e93083692b
> Content-Length: 67913087
> Expect: 100-continue
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 100 Continue
* We are completely uploaded and fine
* Mark bundle as not supporting multiuse
< HTTP/1.1 201 Created
< Server: Artifactory/6.12.0
< X-Artifactory-Id: 422b7f3a6c2dda57:-678bb890:16cd4997ee8:-8000
< Location: http://localhost:8086/artifactory/libs-release-local/example.jar
< Content-Type: application/vnd.org.jfrog.artifactory.storage.ItemCreated+json;charset=ISO-8859-1
< Transfer-Encoding: chunked
< Date: Tue, 27 Aug 2019 21:03:01 GMT
<
{
  "repo" : "libs-release-local",
  "path" : "/example.jar",
  "created" : "2019-08-27T21:03:01.052Z",
  "createdBy" : "admin",
  "downloadUri" : "http://localhost:8086/artifactory/libs-release-local/example.jar",
  "mimeType" : "application/java-archive",
  "size" : "67913087",
  "checksums" : {
    "sha1" : "3310293b545f32644aa55a4509d8b3e93083692b",
    "md5" : "b31fd78f3fe6f41521dea5bd08df06bc",
    "sha256" : "b0a03a8de8fc4f70b41ea4b6882c935ded66b854a7a3ef68fe9a1b888a9c0673"
  },
  "originalChecksums" : {
    "sha1" : "3310293b545f32644aa55a4509d8b3e93083692b",
    "md5" : "b31fd78f3fe6f41521dea5bd08df06bc",
    "sha256" : "b0a03a8de8fc4f70b41ea4b6882c935ded66b854a7a3ef68fe9a1b888a9c0673"
  },
  "uri" : "http://localhost:8086/artifactory/libs-release-local/example.jar"
* Connection #0 to host localhost left intact
}
```
