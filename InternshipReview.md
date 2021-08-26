# Jetfire
## System Artitecture
- admin API/service API/User API
- Jetfire Database(File metadata storage)/Jetfire/Bussiness Directory(Role Permission Check)
- Google GCS/Aliyun OSS/Amazon S3

## Application Service Interface
### UploadFile
流式上传文件。
通过base64编码上传下载文件时，文件内容是请求、回复正文的一部分，需要全部放在内存中，当文件比较大时就会出现问题。因此针对大文件我们需要使用流式API。  
流式API的实现利用了HTTP multipart传输协议。  
返回值包含云服务返回的uri，凭此地址进行访问。  
  
当使用流式上传API时，如果上传的文件是图片且指定了图片处理参数，则会根据参数内容对图片进行处理。  
图片处理包括两类：
- 对原图的处理（脱敏、保留原图）
- 缩放  
  
图片处理的具体实现是通过调用im4java这个第三方库完成的。im4java本身只是对imageMagick命令行工具的包装，因此Jetfire的运行环境需要安装ImageMagick命令行工具，我们可以通过一个定制化的docker镜像实现。

compute SHA-1 digest while inputstream is consumed:
- DigestInputStream
#### DownloadFile
流式下载文件
### Multipart/form-data
可用于HTML表单从浏览器发送信息给服务器。作为多部分文档格式，它由边界线划分出的不同部分组成。每一部分都有自己的实体。以及自己的HTTP请求头。 Content-Disposition和Content-Type用于文件上传领域。
### 多云适配
```
public interface FileObjectStorage{
    String putFile(Inputstream stream) throws FileStorageException;
    InputStream getFileStream(String uri) throws FileStorageException;
    FileObjectBackendStorageType getType();
}
```
使用上述通用接口，根据各云平台分别实现这一接口，并把这些实现注册到一个类型为key的HashMap中，就可以在运行时选择每一个文件存储的后端及其实现。

# TOTP
auth-hub提供三种登录：
- single sign on
- one time password
- time-based one time password
其中OTP和SSO主要是由是否有SSO权限、登录设备是否和上次一致以及是否超出验证时效来决定的

