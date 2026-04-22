# INTRODUCTION

##

## What is OC.PowerSort?

OC.PowerSort extends Umbraco's native content tree functionality by providing advanced sorting features that go beyond simple alphabetical or creation date ordering. The package allows content editors to:

* **Sort content nodes** using various criteria and custom providers
* **Schedule sorting changes** to occur at specific dates and times
* **Create recurring sorting schedules** that automatically apply on a recurring basis
* **Set priorities** to control content order when multiple items have the same sort position
* **Define default sort orders** that automatically apply to new content

## Key Features

### 1. Enhanced Content Sorting

* Multiple sorting strategies available out-of-the-box
* Drag-and-drop interface for manual sorting
* Visual tree representation of content structure
* Apply sorting to any parent node's children

### 2. Schedule Management

* **One-time Schedules**: Set content to move to a specific position at a future date/time
* **Recurring Schedules**: Define patterns for content to automatically reorder on a recurring basis
  * Daily recurrence
  * Weekly recurrence (specific days of the week)
  * Monthly recurrence (specific day of month or day of week pattern)
  * Custom intervals
* **Schedule Duration**: Control how long a boosted position remains active
* **Schedule End Dates**: Set when recurring schedules should stop
* **Maximum Occurrences**: Limit the number of times a recurring schedule runs

### 3. Priority System

When multiple content items share the same sort order position, the priority system determines which item appears first. This is particularly useful when combined with schedules, allowing editors to boost important content temporarily.

### 4. Default Sort Orders

Define default sorting behavior for specific parent nodes, ensuring consistent content ordering without manual intervention each time new content is added.

### 5. Extensible Provider System

Developers can create custom sort providers to implement business-specific sorting logic:

* **ISortProvider Interface**: Clean abstraction for implementing custom sorting strategies
* **Built-in Examples**:
  * `DefaultScheduleSortProvider`: Standard schedule-based sorting
  * `AlphabeticalSortProvider`: Alphabetical ordering
  * `NewestFirstSortProvider`: Sort by creation date
  * `FeaturedContentBoostProvider`: Boost featured content
  * `PopularityBoostProvider`: Sort by popularity metrics
* **Provider Factory**: Automatic discovery and registration of custom providers

## Architecture

### Core Components

**Services:**

* `ScheduleService`: Manages schedule CRUD operations
* `ScheduleProcessingService`: Executes scheduled sorting operations
* `RecurrenceCalculatorService`: Calculates occurrence dates for recurring schedules
* `OccurrenceGenerationService`: Generates schedule occurrences from recurring patterns
* `SortProviderFactory`: Discovers and instantiates sort providers
* `SortingFlagService`: Manages sorting flags and default behaviors

**Controllers:**

* `ScheduleAPIController`: REST API for schedule management
* `RecurringScheduleApiController`: REST API for recurring schedule operations
* `ChildrenAndSortingAPIController`: API for retrieving and sorting content trees
* `MenuItemsApiController`: Provides menu items for the backoffice interface
* `EnumPriorityAPIController`: Manages priority enumeration values

**Models:**

* `SortScheduleModel`: Represents a one-time scheduled sort operation
* `RecurringScheduleDto`: Database model for recurring schedules
* `ScheduleOccurrence`: Individual occurrence generated from recurring schedules

### Database Structure

OC.PowerSort creates several database tables to persist sorting information:

* `ocPowerSortSchedule`: Stores one-time scheduled sort operations
* `ocPowerSortRecurringSchedule`: Stores recurring schedule patterns
* `ocPowerSortScheduleOccurrence`: Individual occurrences generated from recurring schedules
* `ocPowerSortDefaultSortOrder`: Default sorting behavior for parent nodes
* `ocPowerSortEnumPriority`: Priority enumeration values

## Technical Requirements

* **Umbraco Version**: 17+
* **.NET Version**: 10
* **Database**: SQL Server (compatible with Umbraco's database requirements)

## Use Cases

### Content Promotion

Automatically promote specific content items during campaigns or events. For example, boost a "Summer Sale" page every weekend during June and July.

### Time-Sensitive Content

Schedule content to appear at the top of listings when it becomes relevant. News articles can automatically move to prominent positions when published, then return to chronological order after a set duration.

### Event Management

Use recurring schedules to automatically promote event pages in the days leading up to events, ensuring users see upcoming events without manual intervention.

### Seasonal Content

Set up recurring schedules to automatically reorder content based on seasonal relevance, such as promoting holiday-related content during specific months.

### Editorial Workflows

Content editors can schedule sorting changes in advance, allowing for planned content strategies without requiring developer involvement or manual updates at specific times.

## Integration

### Backoffice Integration

The package adds a dedicated "PowerSort" section to the Umbraco backoffice, providing a dedicated workspace for managing sorting operations.

### Frontend Implementation

OC.PowerSort updates the underlying `sortOrder` property of Umbraco content nodes. Frontend implementation is handled by developers using standard Umbraco content queries:

```csharp
// Content will automatically be returned in the sort order defined by PowerSort
@foreach(var child in Model.Children())
{
    <div>@child.Name</div>
}
```

### API Integration

RESTful APIs are available for programmatic access to scheduling and sorting functionality, enabling integration with external systems or custom backoffice extensions.

## Extensibility

### Creating Custom Sort Providers

Developers can implement custom sorting logic by creating classes that implement the `ISortProvider` interface:

```csharp
public interface ISortProvider
{
    string ProviderKey { get; }          // Unique identifier
    string DisplayName { get; }          // UI display name
    string Description { get; }          // Provider description
    bool SupportsScheduling { get; }     // Whether scheduling is supported
    
    Task<SortResult> CalculateSortOrderAsync(SortContext context);
    Task<ProviderValidationResult> ValidateAsync();
}
```

Custom providers can:

* Integrate with external systems (CRM, analytics, weather APIs, etc.)
* Implement business-specific sorting rules
* Combine multiple data sources for sorting decisions
* Provide validation for configuration requirements

### Provider Registration

Custom providers are automatically discovered and registered through the composer system. Simply implement `ISortProvider` and register it in the DI container.

## Benefits

1. **Editor Empowerment**: Content editors can manage content presentation without developer assistance
2. **Time Efficiency**: Schedule sorting changes in advance, reducing manual workload
3. **Consistency**: Default sort orders ensure consistent content presentation
4. **Flexibility**: Extensible provider system allows custom sorting strategies
5. **Automation**: Recurring schedules eliminate repetitive manual tasks
6. **Predictability**: Scheduled changes occur exactly when planned, every time

## Getting Started

1. **Installation**: Install the NuGet package `OC.PowerSort`
2. **User Permissions**: Grant access to the "PowerSort" section for relevant user groups
3. **Configuration**: Define default sort orders for parent nodes (optional)
4. **Usage**: Navigate to the PowerSort section and start scheduling sorting operations

## Resources

* **GitHub Repository**: [https://github.com/OwainWilliams/OC.PowerSort](https://github.com/OwainWilliams/OC.PowerSort)
* **NuGet Package**: [https://www.nuget.org/packages/OC.PowerSort/](https://www.nuget.org/packages/OC.PowerSort/)
* **Video Tutorials**: Available in the README
* **License**: MIT

## Support and Community

For questions, issues, or contributions, please visit the GitHub repository or consult the contributing guidelines.

## Credits

**Created by:**

* [Owain Williams](https://github.com/OwainWilliams/)
* [Harrie Mayhew](https://github.com/mayhemcreates)

**License:** MIT License
