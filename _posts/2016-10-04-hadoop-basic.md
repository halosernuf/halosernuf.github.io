---
layout: post
title: "Hadoop Basic Shell"
categories: Hadoop
tags: hadoop shell
---

**mkdir**

* Usage: hadoop fs -mkdir [-p] `<paths>`
    * Takes path uri’s as argument and creates directories.
* Options:
    * The -p option behavior is much like Unix mkdir -p, creating parent directories along the path.
* Example:
    * hadoop fs -mkdir /user/hadoop/dir1 /user/hadoop/dir2
    * hadoop fs -mkdir hdfs://nn1.example.com/user/hadoop/dir hdfs://nn2.example.com/user/hadoop/dir
* Exit Code:
    * Returns 0 on success and -1 on error.

**cat**

* Usage: hadoop fs -cat URI [URI ...]
    * Copies source paths to stdout.
* Example:
    * hadoop fs -cat hdfs://nn1.example.com/file1 hdfs://nn2.example.com/file2
    * hadoop fs -cat file:///file3 /user/hadoop/file4
* Exit Code:
    * Returns 0 on success and -1 on error.

**checksum**

* Usage: hadoop fs -checksum URI
    * Returns the checksum information of a file.
* Example:
    * hadoop fs -checksum hdfs://nn1.example.com/file1
    * hadoop fs -checksum file:///etc/hosts

**put**

* Usage: hadoop fs -put <localsrc> ... <dst>
    * Copy single src, or multiple srcs from local file system to the destination file system. Also reads input from stdin and writes to destination file system.
* Example: 
    * hadoop fs -put localfile /user/hadoop/hadoopfile
    * hadoop fs -put localfile1 localfile2 /user/hadoop/hadoopdir
    * hadoop fs -put localfile hdfs://nn.example.com/hadoop/hadoopfile
    * hadoop fs -put - hdfs://nn.example.com/hadoop/hadoopfile Reads the input from stdin.
* Exit Code:
    * Returns 0 on success and -1 on error.

**copyFromLocal**

* Usage: hadoop fs -copyFromLocal `<localsrc>` URI
    * Similar to put command, except that the source is restricted to a local file reference.
* Options:
    * The -f option will overwrite the destination if it already exists.

**copyToLocal**

* Usage: hadoop fs -copyToLocal [-ignorecrc] [-crc] URI <localdst>
    *Similar to get command, except that the destination is restricted to a local file reference.

**rm**

* Usage: hadoop fs -rm [-f] [-r]/[-R] [-skipTrash] URI [URI]
    * Delete files specified as args.
    * If trash is enabled, file system instead moves the deleted file to a trash directory (given by FileSystem#getTrashRoot).
    * Currently, the trash feature is disabled by default. User can enable trash by setting a value greater than zero for parameter fs.trash.interval (in core-site.xml).
    * See expunge about deletion of files in trash.

* Options:
    * The -f option will not display a diagnostic message or modify the exit status to reflect an error if the file does not exist.
    * The -R option deletes the directory and any content under it recursively.
    * The -r option is equivalent to -R.
    * The -skipTrash option will bypass trash, if enabled, and delete the specified file(s) immediately. This can be useful when it is necessary to delete files from an over-quota directory.
* Example:
    * hadoop fs -rm hdfs://nn.example.com/file /user/hadoop/emptydir
* Exit Code:
    * Returns 0 on success and -1 on error.

**rmdir**

* Usage: hadoop fs -rmdir [--ignore-fail-on-non-empty] URI [URI ...]
    * Delete a directory.
* Options:
    * --ignore-fail-on-non-empty: When using wildcards, do not fail if a directory still contains files.
* Example:
    * hadoop fs -rmdir /user/hadoop/emptydir