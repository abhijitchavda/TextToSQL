# TextToSQL

# TextToSQL

TextToSQL is a powerful tool designed to convert natural human language into SQL queries. Leveraging LangChain and Ollama, it can generate, explain, and execute SQL queries against a specified database. This project streamlines database interactions, making it easier for users without SQL expertise to retrieve and manipulate data.

## Features

- **Natural Language to SQL Conversion**: Converts user input in plain English into a valid SQL query.
- **Query Explanation**: Provides a detailed explanation of the generated SQL query.
- **Query Execution**: Executes the generated SQL query against the connected database.
- **User Interaction**: Allows users to choose whether to execute the query, get an explanation, or abort the operation.
- **Dynamic few-shot prompting**: Dynamically chooses examples that best matches with the user question by using similarity search. Uses these examples to generate a few-shot prompt.
- **Examples Generation**: Creates a set of natural language questions and their corresponding SQL queries for a specified database, used for dynamic few-shot prompting in SQL query generation.

## How It Works

1. **Query Generation**:
   - The user inputs a question in natural language.
   - `query_chain` validates the question and generates an SQL query using `write_query_chain` and `llm_approval`.

2. **User Interaction**:
   - The system asks the user to choose an action:
     - Execute the query.
     - Get an explanation of the query.
     - Abort the operation.

3. **Action Execution**:
   - If the user chooses to execute the query, `execute_query_chain` runs the SQL query against the database and returns the results.
   - If the user asks for an explanation, `explain_chain` provides a detailed breakdown of the SQL query.
   - The loop continues until the user decides to execute the query or abort the operation.

## Example

1. **Input**:
   ```
   What is the total revenue generated from selling Ford Mustang?
   ```

2. **Generated SQL Query**:
   ```sql
   SELECT SUM(price * quantity) as total_revenue FROM sales JOIN cars ON sales.carid = cars.carid WHERE cars.make = 'Ford' AND cars.model = 'Mustang';
   ```

3. **User Actions**:
   - Execute the query to get results.
    ```
    [(Decimal('112051.12'),)]
    ```
   - Get an explanation:
     ```
     This query calculates the total revenue for Ford Mustand car sales by summing the product of price and qunatity sold from the 'sales' table, joining it with the 'cars' table where the car ID matches, and filtering results based on make ('Ford') and model ('Mustang').
     ```

## License

This project is licensed under the MIT License.

---

Feel free to customize this README to better fit your project's specifics and structure.