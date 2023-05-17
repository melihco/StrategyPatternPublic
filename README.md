We have the `IShippingStrategy` interface, which defines the contract for different shipping strategies. The `StandardShippingStrategy` and `ExpressShippingStrategy` are concrete implementations of the strategy interface.

The `ShippingContext` class acts as the context that uses the selected strategy to calculate the shipping cost. It has a method to set the strategy dynamically and another method to calculate the shipping cost based on the selected strategy.

In the `Main` method, we create an instance of the `ShippingContext` and set the strategy to `StandardShippingStrategy`. We then calculate the shipping cost for a given weight. After that, we change the strategy to `ExpressShippingStrategy` and calculate the shipping cost again. The output displays the shipping costs based on the selected strategies.

The Strategy Pattern allows us to encapsulate different algorithms or behaviors (shipping strategies in this case) and switch between them dynamically at runtime. It promotes flexibility and modularity in the code by separating the behavior from the context.

```csharp
using System;

// Step 1: Define the strategy interface
public interface IShippingStrategy
{
    double CalculateShippingCost(double weight);
}

// Step 2: Implement concrete strategies
public class StandardShippingStrategy : IShippingStrategy
{
    public double CalculateShippingCost(double weight)
    {
        // Standard shipping calculation logic
        return weight * 1.5;
    }
}

public class ExpressShippingStrategy : IShippingStrategy
{
    public double CalculateShippingCost(double weight)
    {
        // Express shipping calculation logic
        return weight * 3;
    }
}

// Step 3: Define the context
public class ShippingContext
{
    private IShippingStrategy _shippingStrategy;

    public void SetShippingStrategy(IShippingStrategy strategy)
    {
        _shippingStrategy = strategy;
    }

    public double CalculateShippingCost(double weight)
    {
        if (_shippingStrategy == null)
        {
            throw new InvalidOperationException("Shipping strategy has not been set.");
        }

        return _shippingStrategy.CalculateShippingCost(weight);
    }
}

// Step 4: Usage example
class Program
{
    static void Main(string[] args)
    {
        // Create the context
        var context = new ShippingContext();

        // Set the strategy dynamically
        context.SetShippingStrategy(new StandardShippingStrategy());

        // Calculate the shipping cost using the selected strategy
        double weight = 10;
        double shippingCost = context.CalculateShippingCost(weight);
        Console.WriteLine($"Shipping cost for weight {weight}kg: ${shippingCost}");

        // Change the strategy dynamically
        context.SetShippingStrategy(new ExpressShippingStrategy());

        // Calculate the shipping cost using the new strategy
        shippingCost = context.CalculateShippingCost(weight);
        Console.WriteLine($"Shipping cost for weight {weight}kg: ${shippingCost}");
    }
}
```

