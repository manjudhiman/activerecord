# activerecord

# Introduction to ActiveRecord


ActiveRecord is an ORM (Object Relational Mapping). It is basically Ruby code that exists between database and the logic code.

When we need to update the database, we need to write ruby code and then needs to run rails db:migrate to reflect the changes to the database.


### Command to generate the migrations

  
  ```
  rails g model Table table_field
  ```
  
  
  The above command generates the model and migration with the table_name. Something like 
  ```
  create	db/migrate/20180213204626_create_table.rb
  create	app/models/table.rb
  ```
  
  
  But in reality it calls the [model_generator.rb|https://github.com/rails/rails/blob/master/activerecord/lib/rails/generators/active_record/model/model_generator.rb#L18] and [migration_file|https://github.com/rails/rails/blob/master/activerecord/lib/rails/generators/active_record/migration/templates/create_table_migration.rb.tt]
  that helps in creating the above files.
  
  Once the model and migrations are created we have to run:
  ```
  rails db:migrate
  ```
  This command will generate the migrations.
  
  Now the migrations has been generated, we need to store the data to database.
  ```
  t = Table.new table_field: 'test'
  ```
  This will create the instance of the Table, but it has not been saved yet so to save it. we need to run
  
  ```
  t.save
  ```
  
  Now the data entered is saved to the database. This is equivalent to running the SQL query in the backend. Inside the abstract adapter [this method|https://github.com/rails/rails/blob/master/activerecord/lib/active_record/connection_adapters/abstract/database_statements.rb#L139] will run the Insert query and save to database.