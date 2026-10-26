## Step 1: 

- The website's name: Youtube 
- The website's URL: https://www.youtube.com/
- One or two features you will test: Search Bar Operators, Video Playback Speed

## Step 2:
Equivalence Partitioning (For Video Playback Speed)
- Valid partitions:  
    - `0.25` - `2.00` (Regular)
    - `0.25` - `3.00` (Youtube Premium)
- Invalid partitions: 
   - < `0.25` (Regular & Youtube Premium)
   - > `2.00` (Regular)
   - > `3.00` (Youtube Premium)
- One representative value from each partition & Expected Result:
    - `2.00` (Valid Regular)
    - `3.00` (Valid Youtube Premium) 
    - `0.05` (Invalid Regular & Youtube Premium)
    - `4.00` (Invalid Youtube Premium) 

## Step 3: 
Decision Table (For Video Playback Speed)
- Conditions:
    - Is On a Youtube Video? 
    - Has Youtube Premium? 
- Actions:
    - Access Premium Video Playback Speeds
    - Access Regular Video Playback Speeds
- Completed Decision Table:
|                                         |           1           |          2          |         3            |          4          |
| --------------------------------------- | --------------------- | ------------------- | -------------------  | ------------------- |
|**On a Youtube Video?**                  |           T           |          F          |         F            |          T          |
|**Has Youtube Premium?**                 |           F           |          F          |         T            |          T          |
| ----------------------------------------| --------------------- | ------------------- | -------------------- | --------------------|
| **Access Premium Video Playback Speeds**|                       |                     |                      |          X          |
| **Access Regular Video Playback Speeds**|           X           |                     |                      |          X          |

- Test cases:
    - **TC-01**: Youtube Video w/o Youtube Premium
        - On a Youtube Video?: T 
        - Has Youtube Premium?: F 
        - Expected Result: Have access to regular playback speeds
    - **TC-02**: All Invalid Conditions 
        - On a Youtube Video?: F 
        - Has Youtube Premium?: F 
        - Expected Result: No access to playback speeds 
    - **TC-03**: Youtube Premium w/o Youtube Video 
        - On a Youtube Video?: F 
        - Has Youtube Premium?: T 
        - Expected Result: No access to playback speeds 
    - **TC-04**: Youtube Video With Youtube Premium   
        - On a Youtube Video?: T 
        - Has Youtube Premium?: T 
        - Expected Result: Have access to regular & premium playback speeds


## Step 4: 
State Transition Testing (Youtube Search Bar) 
- States
    - `Exact Phrase` Operator (" ")
    - `Exclude Word` Operator ( - )
    - `Shorts filter`  Videos Operator (short)
    - `Live filter` Streams Operator (live)
    - Videos uploaded `Before` Operator (before:)
    - `Unfiltered` Search
    - `Empty` Search Bar
- Events
    - Entering `Exact Phrase` Operator (e.g., "lofi hip hop")
    - Entering `Exclude Word` Operator (e.g., SEO -tools)
    - Entering `Shorts filter` Operator (e.g., *search term* short)
    - Entering `Live filter` Operator (e.g., *search term* live)
    - Append `Before` Operator (e.g., vlogs before:2025-01-01)
    - Invalid Operator Entries 
- Valid and invalid transitions: 
    - Valid: Using search operators correctly (as shown in events)
    - Invalid: Not using search operators correctly `SearchQueryError`

- State Transition Table: 
| Current State  | Event                                              | Expected State     | Expected Result                                     |
| -------------  | -------------------------------------------------- | ------------------ | --------------------------------------------------- |
| Empty          | Typing "lofi hip hop" in Search Bar                | `Exact Phrase`     | Searches for an exact string match of the query     |
| Empty          | Typing SEO -tools in Search Bar                    | `Exclude Word`     | Searches query that excludes "tools"                |
| Empty          | Typing Brownie recipe shorts in Search Bar         | `Shorts filter`    | Searches for brownie recipes in shorts format       |
| Empty          | Typing IShowSpeed Live in Search Bar               | `Live filter`      | Search results show IShowSpeed in livestream format |
| Empty          | Typing vlogs before:2025-01-01                     | `Before`           | Search results show vlogs uploaded before 2025-01-01|
| Before         | Search query for vlogs before:Jan-1                | `Unfiltered`       | Unfiltered search result, `SearchQueryError`        |
| Exclude Word   | Search query for SEO - tools                       | `Unfiltered`       | Unfiltered search result, `SearchQueryError`        |
| Exact Word     | Search query for "lofi hip hop                     | `Unfiltered`       | Unfiltered search result, `SearchQueryError`        |

- Test Cases: 
| Test ID | Current State  | Event                                              | Expected State     | Expected Result                                     | Transition Type |                
| ------- |--------------- | -------------------------------------------------- | ------------------ | --------------------------------------------------- | --------------- |
| ST01    | Empty          | Typing "lofi hip hop" in Search Bar                | `Exact Phrase`     | Searches for an exact string match of the query     | Valid           |
| ST02    | Empty          | Typing SEO -tools in Search Bar                    | `Exclude Word`     | Searches query that excludes "tools"                | Valid           |
| ST03    | Empty          | Typing Brownie recipe shorts in Search Bar         | `Shorts filter`    | Searches for brownie recipes in shorts format       | Valid           |
| ST04    | Empty          | Typing IShowSpeed Live in Search Bar               | `Live filter`      | Search results show IShowSpeed in livestream format | Valid           |
| ST05    | Empty          | Typing vlogs before:2025-01-01                     | `Before`           | Search results show vlogs uploaded before 2025-01-01| Valid           |
| ST06    | Before         | Search query for vlogs before:Jan-1                | `Unfiltered`       | Unfiltered search result, `SearchQueryError`        | Invalid         |
| ST07    | Exclude Word   | Search query for SEO - tools                       | `Unfiltered`       | Unfiltered search result, `SearchQueryError`        | Invalid         |
| ST08    | Exact Word     | Search query for "lofi hip hop                     | `Unfiltered`       | Unfiltered search result, `SearchQueryError`        | Invalid         |