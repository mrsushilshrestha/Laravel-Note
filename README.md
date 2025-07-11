# Laravel: Creating a Model and Migration using Artisan 
This guide walks you through creating a **Model** and **Migration** in Laravel using the Artisan CLI.

---

## 🔧 Step-by-Step: Create a Model

To create a model in Laravel, use the following command:

```bash
php artisan make:model ModelName
```

This will create a model file inside the `app/Models/` directory.

---

## 🧱 Step-by-Step: Create a Migration

To create a migration file for a model, use this command:

```bash
php artisan make:migration create_modelname_table
```

Make sure to follow Laravel’s naming convention (`create_<table_name>_table`) to avoid issues with schema builder.

---

## 📦 Example

### Create a Model and Migration Separately

```bash
php artisan make:model ExampleModel
php artisan make:migration create_example_model_table
```

---

## 🚀 Shortcut: Create Model with Migration

You can also create both the model and the migration file at the same time using the `-m` flag:

```bash
php artisan make:model ExampleModel -m
```

This command will:

* Create the model file `app/Models/ExampleModel.php`
* Generate a migration file like `xxxx_xx_xx_xxxxxx_create_example_models_table.php` in `database/migrations/`

---

## 🧑‍🎓 Example: Student Model and Migration

### Command:

```bash
php artisan make:model Student -m
```

### Model File: `Student.php`

```php
class Student extends Model
{
    protected $fillable = ["username", "name", "sex", "age", "address", "class", "nationality"];
}
```

### Migration File:

```php
Schema::create('students', function (Blueprint $table) {
    $table->id();
    $table->string('username', 200);
    $table->string('name', 200);
    $table->string('sex', 8);
    $table->integer('age');
    $table->text('address');
    $table->integer('class');
    $table->string('nationality', 50);
    $table->timestamps();
});
```

---

## ➕ Adding a Field After Migration

If you want to add a new field to an existing table, use the following Artisan command:

```bash
php artisan make:migration add_fieldName_to_tableName_table --table=tableName
```

📌 **Example:**

```bash
php artisan make:migration add_age_to_students_table --table=students
```

This will create a new migration file where you can define the additional field in the `up()` method.

After editing the migration, apply the changes with:

```bash
php artisan migrate
```

To reset and apply all migrations again (use with caution as it clears data):

```bash
php artisan migrate:fresh
```

---

## 🛠️ Troubleshooting: Migration Changes Not Applying

If you make changes to your migration (like editing a column or adding a new one) but the migration doesn't reflect in the database, try this:

1. First, reset all migrations and drop all tables:

```bash
php artisan migrate:fresh
```

2. Then run the migration again:

```bash
php artisan migrate
```

This ensures the latest changes are properly applied.

---

## Done!

Now you can edit your migration file and add the necessary schema structure. Then run:

```bash
php artisan migrate
```

To apply your migration and create the table in the database.

---
