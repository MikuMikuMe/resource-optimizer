# resource-optimizer

Creating a resource optimizer program that analyzes organizational resources and recommends cost-effective allocation strategies involves various steps. Below is a simple Python program that demonstrates the main concepts. We'll use mock data and basic strategy functions to illustrate the idea. In a real-world scenario, this program can be expanded with actual data-dependencies, more sophisticated algorithms, and user inputs.

```python
import random

# Define a class for handling resource data
class Resource:
    def __init__(self, name, cost, usage):
        self.name = name
        self.cost = cost
        self.usage = usage

    def __str__(self):
        return f"Resource(name={self.name}, cost={self.cost}, usage={self.usage})"


class ResourceOptimizer:
    def __init__(self, resources):
        self.resources = resources

    def analyze_resources(self):
        """
        Analyzes resources to determine total cost and average usage.
        """
        try:
            total_cost = sum(resource.cost for resource in self.resources)
            average_usage = sum(resource.usage for resource in self.resources) / len(self.resources)
            return total_cost, average_usage
        except ZeroDivisionError:
            print("Error: No resources available for analysis.")
            return None, None

    def recommend_optimization_strategy(self):
        """
        Recommend a strategy based on the analysis for cost-effective allocation.
        """
        total_cost, average_usage = self.analyze_resources()
        if total_cost is None or average_usage is None:
            return False

        print(f"Total Cost of Resources: ${total_cost}")
        print(f"Average Usage of Resources: {average_usage}%\n")

        # Example of a basic recommendation strategy
        if average_usage < 50:
            print("Recommendation: Re-evaluate resources with low usage and consider reducing or reallocating them.\n")
        elif average_usage > 80:
            print("Recommendation: Optimize high usage resources for better efficiency or consider expanding capacity.\n")
        else:
            print("Resources are being utilized effectively.\n")

    def get_resource_with_max_usage(self):
        """
        Find and return the resource with the maximum usage.
        """
        try:
            max_usage_resource = max(self.resources, key=lambda res: res.usage)
            return max_usage_resource
        except ValueError:
            print("Error: Unable to find the resource with maximum usage, no resources available.")
            return None


# Example usage
def main():
    # Mock data for resources
    resources_data = [
        Resource("Resource1", 1500, random.randint(30, 100)),
        Resource("Resource2", 2200, random.randint(30, 100)),
        Resource("Resource3", 1200, random.randint(30, 100)),
        Resource("Resource4", 3000, random.randint(30, 100))
    ]

    optimizer = ResourceOptimizer(resources_data)

    # Error handling to ensure resources are not empty
    if not resources_data:
        print("Error: Resource list is empty. Please provide resources to analyze.")
        return

    print("Analyzing Resources:")
    optimizer.recommend_optimization_strategy()

    print("Finding Resource with Maximum Usage:")
    max_usage_resource = optimizer.get_resource_with_max_usage()
    if max_usage_resource:
        print(f"Resource with Maximum Usage: {max_usage_resource.name} with {max_usage_resource.usage}% usage.")


if __name__ == "__main__":
    main()
```

### Explanation:

1. **Resource Class**: This defines a `Resource` class to hold the details of individual resources like `name`, `cost`, and `usage`.

2. **ResourceOptimizer Class**: This is the core of the optimization system, containing:
   - `analyze_resources`: Calculates total cost and average usage of resources.
   - `recommend_optimization_strategy`: Makes simple recommendations based on usage.
   - `get_resource_with_max_usage`: Identifies the resource with the highest usage.

3. **Error Handling**: The program includes basic error handling such as for zero resources or divisions, ensuring that the program runs smoothly without crashing.

4. **Main Function**: This is the entry point of the program, where mock data is prepared and the analysis is initiated.

This code can be extended to handle real-world data input, implement complex optimization algorithms, and output detailed reports as per the requirements.