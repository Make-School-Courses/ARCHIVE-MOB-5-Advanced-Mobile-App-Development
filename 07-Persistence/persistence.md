# Intro to Persistence - Keychain & UserDefaults

### Objectives
- NSUserDefaults
- Keychain
- Filesystem
- Encoding/Decoding
- Advanced Persistence Technologies - CoreData, Realm etc.


## UserDefaults

NSUserDefaults allows to store Strings, Numbers, Dates, NSData and
Arrays or Dictionaries

Usually should be used to store user preferences, can be used to store small amount of persistent information

Should never be used for sensitive data

```swift
NSUserDefaults.standardUserDefaults().setBool(false, forKey: "UserAccountCreated")
```

## Keychain

Is used to store sensitive information, such as passwords 

All information is stored encrypted

Apple’s API is arcane - Open Source Libraries such as
SSKeychain will make your life easier!

## Filesystem

Apps can only read/write files within their sandbox

### Important Directories

```
<Application_Home>/AppName.app
```

This is the main bundle of the App. 

All of the content of this
folder is created at compile time (based on files added in
Xcode) and cannot be modified at runtime!

Bundle contains binary along with resource files


```
<Application_Home>/Documents/ 
```

This is the place to store data that is critical to your application
(user generated content, content that cannot be automatically
regenerated)

This directory is backed up with iTunes Backups and it can be
made available to iTunes users via Filesharing

```swift
<Application_Home>/Library/tmp
```

Use this to store files that you do need to to persist
permanently.

You are responsible for removing files from this
directory when they are no longer needed

All files in the Library directory (excluding the Library/Caches
directory) are backed up to iTunes by default. You can change
this by using a file attribute

```swift
<Application_Home>/Library/Caches
```

This folder should be used to store cached information (e.g.
profile pictures that have been downloaded)
iOS will remove file from this directory when it needs to free
disk space, your app needs to be able to handle deletion of
file in the caches directory

The content of this folder is not backed up to iTunes


### Accessing files
Accessing files within the application bundle:
```swift
let path = NSBundle.mainBundle().pathForResource("file1", ofType: ".jpg")
if let path = path {
    let image = UIImage(contentsOfFile:path)
}
```
Short form:`
```swift
UIImage(named: "file1.jpg")
```

#### Accessing files within the documents directory:
```swift
let fileManager = NSFileManager.defaultManager()
let urls = fileManager.URLsForDirectory(.DocumentDirectory,
inDomains: .UserDomainMask)

if let documentDirectory: NSURL = urls.first {
    let documentURL = documentDirectory.URLByAppendingPathComponent("txtFile.txt")
    do {
        let content = try String(contentsOfURL: documentURL)
    } catch let error as NSError {
        print(error.localizedDescription)
    }
}
 ```

### Writing files

Writing a file to the documents directory:

```swift
let fileManager = NSFileManager.defaultManager()
let urls = fileManager.URLsForDirectory(.DocumentDirectory,
inDomains: .UserDomainMask)

if let documentDirectory: NSURL = urls.first {
    let documentURL = documentDirectory.URLByAppendingPathComponent("txtFile.txt")
    // data you want to write to file
    let data = NSData()
    data.writeToURL(documentURL, atomically: true)
}
```

### When to use filesystem

- Primarily when storing/caching binary data such as images
- Can also be used to store serialized Objects, allows to persist
- Objects and Object Graphs from your application

## Encoding/Decoding

Encoding: Creating a binary/textual representation (that can
be stored on disk, transferred via network) from an object
graph

Decoding: Creating an object graph from a binary/textual
representation

### Step 1: Implement NSCoding

```swift
class Movie: NSObject, NSCoding {
    var title: String
    var duration: Int

    init(title: String, duration: Int) {
        self.title = title
        self.duration = duration
    }

    required convenience init?(coder aDecoder: NSCoder) {
        guard let title = aDecoder.decodeObjectForKey("title") as? String,
        let duration = aDecoder.decodeObjectForKey("duration") as? Int
        else { return nil }

        self.init(title: title, duration: duration)
    }

    func encodeWithCoder(coder: NSCoder) {
        coder.encodeObject(self.title, forKey: "title")
        coder.encodeObject(self.duration, forKey: "duration")
    }
}
```

### Step 2: User Archiver

Archive

```swift
NSKeyedArchiver.archiveRootObject(movies, toFile: "/path/to/archive")
```

Unarchive

```
let unarchivedMovies = NSKeyedUnarchiver.unarchiveObjectWithFile(
"/path/to/archive") as? [Movie]
```
 
### When to use NSCoding
Use NSCoding when main goal of persistence in your App is
to store the current state of the application
If you additionally want to create queries, need migrations,
etc, there are better solutions (e.g., CoreData)

## Advanced Persistence Technologies
##### Core Data, Realm, SQLite
- Querying / selecting a subset of object graph
- Saving individual objects independent of entire graph
- Simple versioning of data model

## Summary
- NSUserDefaults is the easiest way to persist a small amount of
information in an application
- Security relevant information should be stored in the Keychain
- Apps run in a sandbox where they have access to their bundle and
different types of directories
- The entire object graph of an application can be persisted using
- NSCoding and NSArchiver; good solution if you merely need to store
the state of your app and don’t need queries or migrations

## Resources