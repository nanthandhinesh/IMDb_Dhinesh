
# IMDb-Dashboard

### Dashboard Link : https://app.powerbi.com/links/Hpgza2ZNK_?ctid=316aa4d3-f4ee-48f0-9ce7-cef2e1e2a331&pbi_source=linkShare&bookmarkGuid=fd587278-8dc7-4916-a7f6-bd0a9cf2eaae

## Problem Statement

This dashboard helps the people to select a movie based on its IMDb ratings as well as the likings of the people's choice. And it helps producers to understand which directors have done better returns and are popular among the public to invest in future. It helps the movie industry as a whole to improve by using the genre that is popular among the public and also people get to choose which movie works for them better. 

Also since average delay in choosing a movie to watch is 10 minutes to 30 minutes, thus this dashbaord help to reduce it.


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present except column named "budget".
- Step 5 : For calculating ratings, null values were not taken into account as only less than 1% values are null in this column(i.e column named "ratings") 
- Step 6 : In the report view, under the view tab, theme was selected.
- Step 7 : Since the data contains various ratings, thus in order to represent ratings, a new visual was added using the three ellipses in the visualizations pane in report view. 
- Step 8 : Visual filters (Slicers) were added for four fields named "genre", "director", "Year of Release" & "Cast members".
- Step 9 : Two graph visuals were added to the canvas, one representing average imdb rating by genre & other representing number of movies released in the year
           Using visual level filter from the filters pane, basic filtering was used & null values were unselected for consideration into average calculation.
           
           Although, by default, while calculating average, blank values are ignored.
- Step 10 : A Deneb visual was also added to the report design area representing the length of the movie with the maximum imdb rating which changes based on the slicers selected. While creating this visual, field named "movielength" was also added to the values section, thus showing the duration of movie on a circular visual using json codes.
- Step 11 : A HTML image viewer was added from appstore and measure called 
"htmlhighestratedmovieURL" which shows the poster of the movie with the highest IMDb rating based on selected slicers.

This was the DAX measure used:
htmlHighestRatedMovieURLnew = 
VAR SelectedYear = SELECTEDVALUE('movies clean'[Release Year])
VAR SelectedGenre = SELECTEDVALUE('movies clean'[Genre])
VAR SelectedCastMember = SELECTEDVALUE('movies clean'[Cast members])

VAR FilteredTable =
    FILTER(
        'movies clean',
        (ISBLANK(SelectedYear) || 'movies clean'[Release Year] = SelectedYear) &&
        (ISBLANK(SelectedGenre) || 'movies clean'[Genre] = SelectedGenre) &&
        (ISBLANK(SelectedCastMember) || 'movies clean'[Cast members] = SelectedCastMember)
    )

VAR TopMovie =
    TOPN(
        1,
        FilteredTable,
        'movies clean'[Rating],
        DESC
    )

VAR PosterURL = MAXX(TopMovie, 'movies clean'[Poster])
VAR MovieURL = MAXX(TopMovie, 'movies clean'[Movie URL])

RETURN
    "<div style='text-align: center;'>
        <a href='" & MovieURL & "' target='_blank'>
            <img src='" & PosterURL & "' style='width: 100%; height: auto; border-radius: 25px;object-fit: cover;'>
        </a>
    </div>"

  
- Step 12 : In the report view, under the insert tab, two text boxes were added to the canvas, in one of them Movie recommendation was mentioned & in the other one Movie success Analysis was written.
- Step 13 : In the report view, under the insert tab, using shapes option from elements group a refresh button was inserted to remove all the slicers done so far. 
- Step 14 : Then a slicer was added and "title" and " movie ratings" are brought into the fields and then reduced the number of rows to be visible to be 1 and number of columns to be made visible to 5 so that we can see the Top 5 picks of the selected filters.
- Step 15: Then a "back" button was added for the page navigation to move to the " home page" at any point of time.
 - Step 16 : The report was then published to Power BI Service.
 
 
![Screenshot 2024-06-14 002819](https://github.com/nanthandhinesh/IMDb_Dhinesh/assets/172712354/9c0c0318-7e94-40df-8511-bd448037d63b)

# Snapshot of Dashboard (Power BI Service)

![Screenshot 2024-06-14 002958](https://github.com/nanthandhinesh/IMDb_Dhinesh/assets/172712354/d8d10176-0b32-4195-9114-4dc81992b24d)



 
 # Report Snapshot (Power BI DESKTOP)

 
![Screenshot 2024-06-14 003018](https://github.com/nanthandhinesh/IMDb_Dhinesh/assets/172712354/719f3820-6c58-41a8-b466-b34935b8cb64)

# Insights

A three page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### [1] Highest rated imdb movie

 
![Screenshot 2024-06-14 003232](https://github.com/nanthandhinesh/IMDb_Dhinesh/assets/172712354/a7a53b3a-bc39-468f-b870-32baf19954f5)
           
### [2] Average Ratings by genre

    
![Screenshot 2024-06-14 003326](https://github.com/nanthandhinesh/IMDb_Dhinesh/assets/172712354/86bed310-3749-4be8-97c8-3dd9b9590d10)

 
  
 
