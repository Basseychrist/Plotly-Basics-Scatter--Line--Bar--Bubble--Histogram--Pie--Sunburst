# Plotly Basics: Data Visualization Tutorial

## Overview

This notebook provides a comprehensive introduction to data visualization using **Plotly**, a powerful Python library for creating interactive charts and graphs. The tutorial is divided into two main sections:

1. **Fundamental Chart Types** - Learning basic visualization techniques with simple datasets
2. **Real-World Application** - Applying visualization skills to the Airline On-Time Performance Dataset

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Libraries Used](#libraries-used)
- [Part I: Fundamental Chart Types](#part-i-fundamental-chart-types)
  - [1. Scatter Plot](#1-scatter-plot)
  - [2. Line Plot](#2-line-plot)
  - [3. Bar Chart](#3-bar-chart)
  - [4. Histogram](#4-histogram)
  - [5. Bubble Plot](#5-bubble-plot)
  - [6. Pie Chart](#6-pie-chart)
  - [7. Sunburst Chart](#7-sunburst-chart)
- [Part II: Airline Dataset Analysis](#part-ii-airline-dataset-analysis)
- [Key Takeaways](#key-takeaways)
- [References](#references)

---

## Prerequisites

- Python 3.x
- Basic understanding of Python programming
- Familiarity with data analysis concepts
- Jupyter Notebook or similar environment

---

## Libraries Used

### 1. **Plotly Graph Objects (`plotly.graph_objects`)**

- **Purpose**: Low-level interface for creating highly customizable visualizations
- **When to use**: When you need fine-grained control over chart elements
- **Key Features**:
  - Manual control of traces, layout, and styling
  - Ideal for complex, custom visualizations
  - More verbose but more flexible

### 2. **Plotly Express (`plotly.express`)**

- **Purpose**: High-level wrapper for Plotly with simplified syntax
- **When to use**: For quick, standard visualizations
- **Key Features**:
  - Concise, one-line chart creation
  - Automatically handles many styling decisions
  - Built on top of graph objects

### 3. **Pandas**

- **Purpose**: Data manipulation and analysis
- **Usage**: Loading, cleaning, and aggregating data

### 4. **NumPy**

- **Purpose**: Numerical computing
- **Usage**: Generating random data for examples

---

## Part I: Fundamental Chart Types

### 1. Scatter Plot

#### Purpose

Scatter plots visualize the relationship between two continuous variables by plotting data points on a two-dimensional plane.

#### When to Use

- Exploring correlations between variables
- Identifying patterns, trends, or outliers
- Comparing two quantitative measurements

#### Example: Income vs Age Analysis

**Dataset**:

- X-axis: Age (25-55 years)
- Y-axis: Income ($300,000-$700,000)

**Code Approach**:

```python
fig = go.Figure()
fig.add_trace(go.Scatter(x=age_array, y=income_array,
                         mode='markers',
                         marker=dict(color='blue')))
fig.update_layout(title='Economic Survey',
                  xaxis_title='Age',
                  yaxis_title='Income')
```

**Key Insights**:

- Uses `go.Figure()` to create an empty figure
- `add_trace()` adds the scatter plot layer
- `mode='markers'` specifies point visualization (vs. lines)
- `update_layout()` customizes titles and labels

**Analysis Result**: The visualization reveals that income is NOT correlated with age in this dataset - income levels remain relatively constant across different age groups.

**Real-World Applications**:

- Height vs. Weight analysis in health studies
- Engine size vs. automobile price in automotive industry
- Study hours vs. exam scores in education

---

### 2. Line Plot

#### Purpose

Line plots display data points connected by lines, ideal for showing trends over time or continuous sequences.

#### When to Use

- Time series data analysis
- Tracking changes over continuous intervals
- Showing progression or trends

#### Example: Bicycle Sales Analysis

**Dataset**:

- X-axis: Months (Jan-Aug)
- Y-axis: Number of bicycles sold

**Code Approach**:

```python
fig = go.Figure()
fig.add_trace(go.Scatter(x=months_array, y=numberofbicyclessold_array,
                         mode='lines',
                         marker=dict(color='green')))
```

**Key Insights**:

- Similar structure to scatter plot
- `mode='lines'` connects data points with lines
- Green color provides visual distinction

**Analysis Result**: Sales peak in May (160 units) followed by a decline through August (45 units), suggesting seasonal patterns or market saturation.

**Business Implications**:

- May requires increased inventory
- Post-May period may need marketing campaigns
- Understanding seasonal trends for better planning

**Real-World Applications**:

- Stock market trends
- Website traffic over time
- Temperature changes throughout the year
- Company revenue growth

---

### 3. Bar Chart

#### Purpose

Bar charts compare categorical data using rectangular bars where length represents the value.

#### When to Use

- Comparing discrete categories
- Showing differences between groups
- Displaying ranked data

#### Example: Student Performance Analysis

**Dataset**:

- X-axis: Grade levels (6-10)
- Y-axis: Pass percentage

**Code Approach**:

```python
fig = px.bar(x=grade_array, y=score_array,
             title='Pass Percentage of Classes')
```

**Key Insights**:

- Uses Plotly Express for simpler syntax
- Single function call creates complete chart
- Automatically handles bar styling

**Analysis Result**:

- Grade 8 shows lowest performance (56%)
- Grade 10 achieves highest scores (95%)
- Suggests need for targeted intervention in Grade 8

**Educational Implications**:

- Resource allocation priorities
- Curriculum difficulty assessment
- Teacher training needs

**Real-World Applications**:

- Sales comparison across products
- Population by country/state
- Survey response distributions
- Movie ratings comparison

---

### 4. Histogram

#### Purpose

Histograms display the distribution of continuous data by grouping values into bins/ranges.

#### When to Use

- Understanding data distribution
- Identifying data patterns (normal, skewed, bimodal)
- Detecting outliers
- Analyzing frequency of occurrences

#### Example: Height Distribution Analysis

**Dataset**:

- 200 people's heights
- Normal distribution (mean=160cm, std=11)

**Code Approach**:

```python
heights_array = np.random.normal(160, 11, 200)
fig = px.histogram(x=heights_array, title="Distribution of Heights")
```

**Key Insights**:

- Uses `np.random.normal()` for realistic data simulation
- Plotly automatically creates bins
- Shows frequency on y-axis

**Analysis Result**:

- Most common height: ~160cm (45 people)
- Distribution follows bell curve
- Very few people at extremes (130cm or 190cm)

**Statistical Significance**:

- Validates normal distribution assumption
- Helps in understanding population characteristics
- Useful for quality control and standardization

**Real-World Applications**:

- Student grade distributions
- Customer age demographics
- Product quality measurements
- Response time analysis
- Income distribution studies

---

### 5. Bubble Plot

#### Purpose

Bubble plots extend scatter plots by adding a third dimension through bubble size, showing relationships between three variables simultaneously.

#### When to Use

- Comparing three related variables
- Showing magnitude with visual emphasis
- Making data more intuitive and engaging

#### Example: Crime Statistics Analysis

**Dataset**:

- X-axis: City names
- Y-axis: Number of crimes
- Bubble size: Total crimes (emphasizes magnitude)

**Code Approach**:

```python
bub_data = df.groupby('City')['Numberofcrimes'].sum().reset_index()
fig = px.scatter(bub_data, x="City", y="Numberofcrimes",
                 size="Numberofcrimes",
                 hover_name="City",
                 size_max=60)
```

**Key Insights**:

- `groupby()` aggregates data by city
- `size` parameter creates bubble effect
- `hover_name` adds interactivity
- `size_max` limits maximum bubble size

**Analysis Result**:

- Chicago: 2,200 total crimes (largest bubble)
- Seattle: 1,850 crimes
- Austin: 1,100 crimes (smallest bubble)

**Visual Advantage**: The bubble size immediately draws attention to high-crime areas, making the comparison intuitive.

**Real-World Applications**:

- Economic indicators (GDP, population, growth rate)
- Market analysis (sales, profit, market share)
- Health data (disease prevalence, mortality rate, population)
- Environmental data (pollution levels, population density, temperature)

---

### 6. Pie Chart

#### Purpose

Pie charts display proportions of a whole, showing how different parts contribute to the total.

#### When to Use

- Showing percentage breakdown
- Comparing parts of a whole
- Limited number of categories (typically 5-7)

#### Example: Household Expenditure Analysis

**Dataset**:

- Categories: Grocery, Rent, School Fees, Transport, Savings
- Values: Percentage of total budget

**Code Approach**:

```python
fig = px.pie(values=exp_percent, names=house_holdcategories,
             title='Household Expenditure')
```

**Key Insights**:

- `values` parameter defines slice sizes
- `names` parameter labels each slice
- Interactive: hover shows exact percentages

**Analysis Result**:

- Rent: 50% (largest expense)
- Grocery: 20%
- Savings: 12%
- School Fees: 10%
- Transport: 8%

**Financial Insights**:

- Housing costs dominate budget
- Limited savings (only 12%)
- Potential areas for cost optimization

**When NOT to Use**:

- Too many categories (hard to read)
- Comparing values that don't sum to 100%
- When precise comparisons are needed (bar charts better)

**Real-World Applications**:

- Market share analysis
- Budget allocation visualization
- Survey response percentages
- Time allocation studies
- Resource distribution

---

### 7. Sunburst Chart

#### Purpose

Sunburst charts visualize hierarchical data as concentric circles, showing parent-child relationships from center outward.

#### When to Use

- Multi-level categorical data
- Organizational structures
- Nested proportions
- Drill-down data exploration

#### Example: Family Tree Visualization

**Dataset**:

- Root: Eve (center)
- Children: Cain, Seth, Abel, Awan, Azura
- Grandchildren: Enos, Noam, Enoch

**Code Approach**:

```python
fig = px.sunburst(data,
                  names='character',
                  parents='parent',
                  values='value',
                  title="Family chart")
```

**Key Insights**:

- `names` defines node labels
- `parents` establishes hierarchy
- `values` determines slice size
- Interactive: click to zoom into sections

**Visual Structure**:

- **Innermost circle**: Root node (Eve)
- **Middle ring**: Direct children
- **Outer rings**: Subsequent generations

**Analysis Result**:

- Visualizes multi-generational relationships
- Slice sizes represent associated values
- Easy to understand complex hierarchies

**Real-World Applications**:

- Corporate organizational charts
- File system visualization
- Product category hierarchies (e-commerce)
- Geographic data (continent → country → city)
- Budget breakdowns (department → team → project)
- Disease outbreak tracking (region → subregion → locality)

---

## Part II: Airline Dataset Analysis

### Dataset Overview

**Source**: U.S. Bureau of Transportation Statistics  
**Size**: ~200 million domestic flights  
**Sample**: 500 randomly selected flights (for analysis efficiency)

**Key Columns**:

- `Distance`: Flight distance in miles
- `DepTime`: Departure time
- `ArrDelay`: Arrival delay in minutes
- `Month`: Month of flight
- `DestState`: Destination state
- `DestStateName`: Full state name
- `Reporting_Airline`: Airline code
- `Flights`: Number of flights
- `DistanceGroup`: Categorized distance ranges

---

### Analysis 1: Distance vs Departure Time (Scatter Plot)

#### Objective

Understand if flight distances influence departure time scheduling.

#### Code Implementation

```python
fig = go.Figure()
fig.add_trace(go.Scatter(x=data['Distance'], y=data['DepTime'],
                         mode='markers',
                         marker=dict(color='red')))
fig.update_layout(title='Distance vs Departure Time',
                  xaxis_title='Distance',
                  yaxis_title='DepTime')
```

#### Key Findings

- **Short distances**: Flights scheduled throughout the day
- **Long distances**: Limited to specific time slots
- **Pattern**: Longer flights concentrate in morning/evening

#### Business Reasoning

1. **Long-haul flights** require:
   - Optimal arrival times (avoid late-night arrivals)
   - Crew rest requirements
   - Airport curfews at destinations
2. **Short-haul flights**: More flexible scheduling

#### Strategic Implications

- Route planning optimization
- Resource allocation
- Customer preference understanding
- Competitive positioning

---

### Analysis 2: Monthly Average Delay (Line Plot)

#### Objective

Identify seasonal patterns in flight delays.

#### Code Implementation

```python
line_data = data.groupby('Month')['ArrDelay'].mean().reset_index()
fig = go.Figure()
fig.add_trace(go.Scatter(x=line_data['Month'], y=line_data['ArrDelay'],
                         mode='lines',
                         marker=dict(color='green')))
```

#### Key Findings

- **Peak delays**: June (summer travel season)
- **Trend**: Delays increase from spring to summer
- **Pattern**: Weather and volume-related

#### Contributing Factors

1. **Summer travel surge**: More passengers = congestion
2. **Weather patterns**: Thunderstorms in summer months
3. **Maintenance schedules**: Spring/fall maintenance windows

#### Operational Recommendations

- Increase buffer time in June schedules
- Enhanced staffing during peak months
- Proactive customer communication
- Dynamic pricing strategies

---

### Analysis 3: Flights by Destination State (Bar Chart)

#### Objective

Identify most popular flight destinations.

#### Code Implementation

```python
bar_data = data.groupby(['DestState'])['Flights'].sum().reset_index()
fig = px.bar(bar_data, x="DestState", y="Flights",
             title='Total number of flights to the destination state')
```

#### Key Findings

- **California (CA)**: 68 flights (highest)
- **Vermont (VT)**: 1 flight (lowest)
- **Pattern**: Coastal and major metropolitan states dominate

#### Market Insights

1. **Population correlation**: More flights to populous states
2. **Economic activity**: Business travel drives demand
3. **Tourism**: Major tourist destinations see high traffic

#### Strategic Applications

- Network planning and route optimization
- Marketing budget allocation
- Partnership opportunities with local businesses
- Hub location decisions

---

### Analysis 4: Arrival Delay Distribution (Histogram)

#### Objective

Understand the distribution and frequency of delays.

#### Code Implementation

```python
data['ArrDelay'] = data['ArrDelay'].fillna(0)
fig = px.histogram(data, x="ArrDelay",
                   title="Arrival Delay Distribution")
```

#### Key Findings

- **Most common**: 20-25 minute delays (17 flights)
- **Severe delays**: 50-54 minutes (5 flights)
- **Distribution**: Right-skewed (most flights on-time or minor delays)

#### Operational Excellence Metrics

- **Target**: Minimize delays over 30 minutes
- **Benchmark**: Compare with industry standards
- **Root causes**: Investigate severe delay patterns

#### Customer Experience Impact

- 20-25 minute delays: Generally tolerable
- 50+ minute delays: Requires compensation/service recovery
- Predictive analytics opportunity for proactive management

---

### Analysis 5: Flights by Airline (Bubble Plot)

#### Objective

Compare airline market presence with visual emphasis.

#### Code Implementation

```python
bub_data = data.groupby('Reporting_Airline')['Flights'].sum().reset_index()
fig = px.scatter(bub_data, x="Reporting_Airline", y="Flights",
                 size="Flights",
                 hover_name="Reporting_Airline",
                 size_max=60)
```

#### Key Findings

- **Southwest (WN)**: 86 flights (market leader)
- **Visual impact**: Bubble size immediately highlights dominance
- **Competition**: Clear market share visualization

#### Competitive Analysis

- Market leader identification
- Entry barrier assessment
- Partnership opportunity evaluation
- Benchmarking against competitors

---

### Analysis 6: Distance Group by Month (Pie Chart)

#### Objective

Understand monthly distribution patterns across distance categories.

#### Code Implementation

```python
fig = px.pie(data, values='Month', names='DistanceGroup',
             title='Distance group proportion by month')
```

#### Key Findings

- **February**: Highest representation in distance groups
- **Pattern**: Seasonal travel preferences visible
- **Proportion**: Different distance categories show varying popularity

#### Travel Pattern Insights

1. **Short-haul popularity**: Certain months favor regional travel
2. **Long-haul seasonality**: International/cross-country peaks
3. **Holiday impact**: February (Valentine's/Presidents Day)

#### Revenue Management

- Dynamic pricing by distance and season
- Capacity allocation optimization
- Promotional campaign timing

---

### Analysis 7: Flight Distribution Hierarchy (Sunburst Chart)

#### Objective

Visualize multi-level data: Month → Destination State → Flight Count

#### Code Implementation

```python
fig = px.sunburst(data, path=['Month', 'DestStateName'],
                  values='Flights',
                  title='Flight Distribution Hierarchy')
```

#### Key Findings

- **Center circle**: Months (root level)
- **Outer rings**: Destination states per month
- **Interactive**: Click months to drill down to states

#### Strategic Value

1. **Multi-dimensional analysis**: See patterns across dimensions
2. **Interactive exploration**: Users discover insights themselves
3. **Capacity planning**: Month-state combinations for resource allocation

#### Decision Support

- Route profitability analysis
- Seasonal route planning
- Marketing campaign targeting (month + destination)
- Crew and aircraft allocation

---

## Key Takeaways

### Technical Skills Developed

1. **Plotly Graph Objects**: Fine-grained control over visualizations
2. **Plotly Express**: Rapid prototyping and standard charts
3. **Data manipulation**: Pandas groupby, aggregation, cleaning
4. **Visual storytelling**: Choosing appropriate chart types

### Analytical Insights

1. **Pattern recognition**: Identifying trends and anomalies
2. **Multi-dimensional analysis**: Exploring data from various angles
3. **Business context**: Translating data insights into actions
4. **Communication**: Presenting data effectively

### Best Practices

#### Chart Selection

| Data Type                | Best Chart | Reason                    |
| ------------------------ | ---------- | ------------------------- |
| Two continuous variables | Scatter    | Shows correlation         |
| Time series              | Line       | Shows trends              |
| Category comparison      | Bar        | Easy comparison           |
| Distribution             | Histogram  | Shows frequency           |
| Three variables          | Bubble     | Size adds dimension       |
| Part-to-whole            | Pie        | Shows proportions         |
| Hierarchical             | Sunburst   | Multi-level relationships |

#### Visualization Guidelines

1. **Keep it simple**: Avoid unnecessary complexity
2. **Label clearly**: Always include titles and axis labels
3. **Use color wisely**: Enhance, don't distract
4. **Provide context**: Add annotations when needed
5. **Make it interactive**: Leverage Plotly's hover features
6. **Consider audience**: Match complexity to viewer expertise

### Common Pitfalls to Avoid

1. **Too many colors**: Stick to 3-5 colors maximum
2. **Missing labels**: Always label axes and provide titles
3. **Wrong chart type**: Ensure chart matches data structure
4. **Overplotting**: Too many data points can obscure patterns
5. **No context**: Provide business context for insights
6. **Ignoring outliers**: Address or explain anomalies

---

## Advanced Techniques

### Customization Options

```python
# Customize marker style
marker=dict(
    color='red',
    size=10,
    symbol='diamond',
    line=dict(width=2, color='black')
)

# Customize layout
fig.update_layout(
    title='Custom Title',
    title_font_size=20,
    xaxis=dict(showgrid=True, gridcolor='lightgray'),
    yaxis=dict(showgrid=True, gridcolor='lightgray'),
    plot_bgcolor='white',
    hovermode='closest'
)
```

### Interactive Features

- **Hover tooltips**: Show additional information
- **Click events**: Drill-down functionality
- **Zoom/pan**: Explore specific regions
- **Legend filtering**: Show/hide data series
- **Export options**: Save as PNG, SVG, etc.

---

## Next Steps

### Further Learning

1. **3D Visualizations**: Explore 3D scatter and surface plots
2. **Animated charts**: Add time dimension with animation
3. **Dashboards**: Combine multiple charts using Dash
4. **Statistical plots**: Box plots, violin plots, correlation matrices
5. **Geospatial visualization**: Maps and choropleth charts

### Project Ideas

1. **Sales dashboard**: Track company performance
2. **COVID-19 tracker**: Visualize pandemic data
3. **Stock portfolio**: Analyze investment performance
4. **Weather patterns**: Climate data visualization
5. **Social media analytics**: Engagement metrics

---

## References

- [Plotly Documentation](https://plotly.com/python/)
- [Plotly Express Documentation](https://plotly.com/python/plotly-express/)
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [Data Visualization Best Practices](https://www.interaction-design.org/literature/article/data-visualization-best-practices)
- [Bureau of Transportation Statistics](https://www.bts.gov/)

---

## Contributing

Feel free to:

- Suggest improvements
- Report issues
- Add new examples
- Share insights from analyses

---

## License

This educational material is provided for learning purposes. Please cite appropriately when using for academic or professional work.

---

**Created by**: IBM Skills Network  
**Last Updated**: 2023  
**Notebook**: 4.3_Plotly_Basics.ipynb
