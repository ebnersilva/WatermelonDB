---
title: Pro Tips
hide_title: true
---

# Various Pro Tips

## Database viewer

[See discussion](https://github.com/Nozbe/WatermelonDB/issues/710)

**Android** - you can use the new [App Inspector](https://medium.com/androiddevelopers/database-inspector-9e91aa265316) in modern versions of Android Studio.

**Via Flipper** You can also use Facebook Flipper [with a plugin](https://github.com/panz3r/react-native-flipper-databases#readme). See [discussion](https://github.com/Nozbe/WatermelonDB/issues/653).

**iOS** - check open database path in iOS System Log (via Console for plugged-in device, or Xcode logs, or [by using `find`](https://github.com/Nozbe/WatermelonDB/issues/710#issuecomment-776255654)), then open it via `sqlite3` in the console, or an external tool like [sqlitebrowser](https://sqlitebrowser.org)

## Prepopulating database on native

There's no built-in support for this. One way is to generate a SQLite DB (you can use the the Node SQLite support in 0.19.0-2 pre-release or extract it from an ios/android app), bundle it with the app, and then use a bit of code to check if the DB you're expecting it available, and if not, making a copy of the default DB — before you attempt loading DB from JS side. [See discussion](https://github.com/Nozbe/WatermelonDB/issues/774#issuecomment-667981361)

## Override entity ID generator

You can optionally overide WatermelonDB's id generator with your own custom id generator in order to create specific random id formats (e.g. if UUIDs are used in the backend). In your database index file, pass a function with your custom ID generator to `setGenerator`:

```
// Define a custom ID generator.
function randomString(): string {
  return 'RANDOM STRING';
}
setGenerator(randomString);

// or as anonymous function:
setGenerator(() => 'RANDOM STRING');
```

To get UUIDs specifically, install [uuid](https://github.com/uuidjs/uuid) and then pass their id generator to `setGenerator`:

```
import { v4 as uuidv4 } from 'uuid';

setGenerator(() => uuidv4());
```
