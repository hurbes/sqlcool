# Sqlcool

A database helper class for [Sqflite](https://github.com/tekartik/sqflite).

Check the [documentation](https://sqlcool.readthedocs.io/en/latest/) for usage instructions

## Quick example

   ```dart
   import 'package:sqlcool/sqlcool.dart';

   void someFunc() async {
      await db.init(dbpath, fromAsset: "assets/db.sqlite", verbose: true).catchError((e) {
          print("Error initializing the database: ${e.message}");
      });
      // insert
      Map<String, String> row = {
       slug: "my-item",
       name: "My item",
      };
      String table = "category";
      db.insert(table, row, verbose: true).catchError((e) {
          print("Error inserting data: ${e.message}");
      });
      // delete
      db.delete(table, "id=3").catchError((e) {
          print("Error deleting data: ${e.message}");
      });
      //update
      Map<String, String> row = {
       slug: "my-item-new",
       name: "My item new",
      };
      String where = "id=1";
      int updated = await db.update(table, row, where, verbose: true).catchError((e) {
          print("Error updating data: ${e.message}");
      // select
      List<Map<String, dynamic>> rows = await db.select(
        table, limit: 20, where: "name LIKE '%something%'",
        orderBy: "name ASC").catchError((e) {
          print("Error selecting data: $e");
      });
   }
   ```

## Todo

- [ ] Better error handling
- [ ] Upsert