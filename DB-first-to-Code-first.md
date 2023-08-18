Migrating from a Database-First approach to a Code-First approach in Entity Framework Core while preserving existing data can be a bit complex, especially when dealing with an existing database schema. Here's a general approach you can follow:

1. **Create the Code-First Models**: Start by creating the Code-First models that represent your existing database schema. You can use the [Database First to Code First](https://www.learnentityframeworkcore.com/walkthroughs/existing-database) guide to help you with this step.

2. **Enable Migrations**: After creating the models, enable migrations for your project using the following command in the Package Manager Console:

   ```bash
   Add-Migration InitialCreate
   ```

3. **Update the Migration**: The generated migration script might need adjustments to match your existing database schema. You might need to modify the generated migration code to ensure it doesn't drop existing tables or data. This could involve:

   - Removing any lines that would drop or recreate existing tables.
   - Modifying the script to update existing columns or constraints instead of recreating them.

4. **Apply the Migration**: Once you're confident that the migration script won't result in data loss, apply the migration to the database using:

   ```bash
   Update-Database
   ```

   This will update your existing database schema to match your new Code-First models.

5. **Handle Data Migration**: If your Code-First models differ significantly from the existing database schema, you might need to write custom data migration scripts to transform and transfer data between old and new schema structures. Entity Framework Core's data migration capabilities are limited compared to its schema migration abilities. You may need to use SQL scripts or other techniques to handle complex data migration scenarios.

6. **Testing and Verification**: Thoroughly test your application to ensure that both the schema and data migrations have been applied correctly and that your application works as expected with the new Code-First models.

Remember that migrating from Database-First to Code-First can be a complex process, especially if there are significant differences between your existing database schema and your new Code-First models. It's crucial to have proper backups of your existing database before performing any migrations to avoid data loss.

It's also important to consider the specific details of your existing database and application before proceeding with such a migration. If the differences between the old and new schema are too significant, it might be more practical to develop a new version of your application with the new schema and perform a data migration from the old database to the new one.
