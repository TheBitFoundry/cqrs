# CQRS

The bit foundry command query responsibility segregation package, to act as a guide for developing database with cqrs transactions that is database agnostic.

## How to use
Common folder structure would look something like below:
|\Commands\
|          \_InsertEmployee.cs
|\Queries\
|         \_FetchEmployee.cs

### Queries

```csharp
// In here liveth a class which should derive from Query. Because the lib supports generic typing we can define our expected return type.
public class FetchEmployee : Query<Employee>
{
  private int Id;
  public FetchEmployee(int id) 
  {
    Id = id;
  }
  // we are ovverriding the base class Execute() method.
  public override void Execute() 
  {
      // Take note. We also have a copy of the IQueryExecutor interface within Query. So, we can make queries to other queries inside a query.
      Result = SelectFirst("SELECT * FROM Employee WHERE Id = @Id;", new { Id = Id });
  }
}

// Definition of Employee
public class Employee 
{
  
}
```
