KVS Schema
==========

KVS Schema is a code generation library to manage key-value data for Android.

I use SharedPreferences to save values. However, sometimes I forget key names and types.
This library helps you to manage key-value data. You can find the structure of pref file at a glance.

How to use KVS Schema
----------

### Create Schema

```java
@Table("example")
public abstract class ExamplePrefsSchema extends PrefSchema {
    @Key("user_id") int userId;
    @Key("user_name") String userName = "guest";

    public static ExamplePrefs create(Context context) {
        return new ExamplePrefs(context);
    }
}
```

Class name should be *Schema for now.

### Write And Read

```java
ExamplePrefs prefs = ExamplePrefsSchema.create(context);
prefs.putUserId(123);
prefs.putUserName("Jack");
prefs.hasUserName(); // => true
prefs.getUserName(); // => Jack
prefs.removeUserName();
prefs.hasUserName(); // => false
```

### Saved XML (the case of PrefSchema)

```xml
root@android:/data/data/com.example.android.kvs/shared_prefs # cat example.xml
<?xml version='1.0' encoding='utf-8' standalone='yes' ?>
<map>
<string name="user_id">123</string>
</map>
```

### Installation

Add dependencies your build.gradle

```groovy
apt 'com.rejasupotaro:kvs-schema-compiler:1.1.0'
compile 'com.rejasupotaro:kvs-schema:1.1.0'
```

### What's going on here?

KVS Schema runs as a standard annotation processor in javac.

For developers
----------

### Show version

```sh
$ ./gradlew version
```

### Bump version

```sh
$ ./gradlew bumpMajor
$ ./gradlew bumpMinor
$ ./gradlew bumpPatch
```

### Generate README

```sh
$ ./gradlew genReadMe
```

### Upload library

```sh
$ ./gradlew bintrayUpload -PdryRun=false
```
