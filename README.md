# Exploring Airbnb Market Trends
![NYC Skyline](nyc.jpg)
Welcome to my project on exploring Airbnb market trends in New York City! New York is one of the most-visited cities in the world, and Airbnb plays a significant role in meeting the high demand for temporary lodging. In this analysis, I explored 2019 Airbnb data to uncover insights into pricing, room types, and reviews. I combined data from multiple formats, including CSV, TSV, and Excel files, to perform this analysis using Python and Jupyter Notebook.

## View the Notebook
You can check out the full analysis here: [View Notebook](https://github.com/caryhtan/Exploring-Airbnb-Market-Trends/blob/master/notebook.ipynb)

## What I Did
I focused on answering the following key questions:
- What is the average price of Airbnb listings in New York City?
- How many private room listings are available?
- What is the range of review dates for the listings?

### Data Sources
I used the following datasets:
1. **data/airbnb_price.csv**
This is a CSV file containing data on Airbnb listing prices and locations.
- **`listing_id`**: unique identifier of listing
- **`price`**: nightly listing price in USD
- **`nbhood_full`**: name of borough and neighborhood where listing is located

2. **data/airbnb_room_type.xlsx**
This is an Excel file containing data on Airbnb listing descriptions and room types.
- **`listing_id`**: unique identifier of listing
- **`description`**: listing description
- **`room_type`**: Airbnb has three types of rooms: shared rooms, private rooms, and entire homes/apartments

3. **data/airbnb_last_review.tsv**
This is a TSV file containing data on Airbnb host names and review dates.
- **`listing_id`**: unique identifier of listing
- **`host_name`**: name of listing host
- **`last_review`**: date when the listing was last reviewed

## What I Found
Here are some key insights I discovered:
- **Average Price**: The average nightly price for Airbnb listings is $141.78.
- **Private Room Count**: There are 11,356 private room listings.
- **Review Dates**:
  - Earliest review: January 1, 2019
  - Latest review: July 9, 2019

## How I Did It
To answer these questions, I:
1. Loaded datasets from CSV, TSV, and Excel files using `pandas`.
2. Merged the datasets on the `listing_id` column to create a single comprehensive table.
3. Cleaned the data, including converting price strings to numeric values and parsing review dates.
4. Calculated key metrics, such as the average price and private room count.

### Example Code
Here’s an example of the code I used:
```python
# Merge datasets
merged = pd.merge(price_df, room_df, on='listing_id')
merged = pd.merge(merged, review_df, on='listing_id')

# Clean and process data
merged['price'] = merged['price'].str.replace(' dollars', '', regex=False).astype(float)
merged['last_review'] = pd.to_datetime(merged['last_review'])

# Key metrics
avg_price = round(merged['price'].mean(), 2)
private_room_count = merged[merged['room_type'].str.lower() == 'private room'].shape[0]
