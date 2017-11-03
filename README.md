# Swifth-Storage Movtivations
1. You can always treat AWS S3 or Aliyun OSS like linux/unix/windows filesystem! You can use most of shell commands.
2. And you can change vender as your wish anytime. More Object Storage provider will be supported later.
3. You can use typical java.io alike API to access the underlay object stroage. Even if you don't know any s3 sdk or oss sdk.
4. Java/Kotlin/Scala are supported.

# CLI
Mimic typical unix-like filesystem commands.

```shell
ls       List files and folders.  
mb       Make a bucket or a folder.  
cat      Display file and object contents.
pipe     Redirect STDIN to an object or file or STDOUT.  
share    Generate URL for sharing.
cp       Copy files and objects.
mirror   Mirror buckets and folders.
find     Finds files which match the given set of parameters.
diff     List objects with size difference or missing between two folders or buckets.
rm       Remove files and objects.
events   Manage object notifications.
watch    Watch for file and object events.
policy   Manage anonymous access to objects.
session  Manage saved sessions for cp command.
config   Manage mc configuration file.
update   Check for a new software update.
version  Print version info.
```

# API

```java
import edu.ustc.swifth.*
```
> Then You can use all APIs of swifth Storage

```java
Swifth.storageType("oss");
Swifth.storageOSS();  // oss
Swifth.storageS3();   // s3
```
> If default filesystems driver is oss, you can skip this step.  
> Both "s3" | "oss", indicates Amazon and aliyun. 

```java
//fetch all files of specified bucket(see upond configuration)
Storage::files($directory);
Storage::allFiles($directory);

Storage::put('path/to/file/file.jpg', $contents); //first parameter is the target file path, second paramter is file content
Storage::putFile('path/to/file/file.jpg', 'local/path/to/local_file.jpg'); // upload file from local path

Storage::get('path/to/file/file.jpg'); // get the file object by path
Storage::exists('path/to/file/file.jpg'); // determine if a given file exists on the storage(OSS)
Storage::size('path/to/file/file.jpg'); // get the file size (Byte)
Storage::lastModified('path/to/file/file.jpg'); // get date of last modification

Storage::directories($directory); // Get all of the directories within a given directory
Storage::allDirectories($directory); // Get all (recursive) of the directories within a given directory

Storage::copy('old/file1.jpg', 'new/file1.jpg');
Storage::move('old/file1.jpg', 'new/file1.jpg');
Storage::rename('path/to/file1.jpg', 'path/to/file2.jpg');

Storage::prepend('file.log', 'Prepended Text'); // Prepend to a file.
Storage::append('file.log', 'Appended Text'); // Append to a file.

Storage::delete('file.jpg');
Storage::delete(['file1.jpg', 'file2.jpg']);

Storage::makeDirectory($directory); // Create a directory.
Storage::deleteDirectory($directory); // Recursively delete a directory.It will delete all files within a given directory, SO Use with caution please.

// upgrade logs
// new plugin for v2.0 version
Storage::putRemoteFile('target/path/to/file/jacob.jpg', 'http://example.com/jacob.jpg'); //upload remote file to storage by remote url
// new function for v2.0.1 version
Storage::url('path/to/img.jpg') // get the file url
```
