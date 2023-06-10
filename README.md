# FIFA-23-Stats-Extraction

I wanted to analyse on how my team performed during a season in FIFA 23. However, FIFA 23 does not save stats on how my team plays throughout a season. Hence, I decided to try and extract out information and compile it to analyse my team's playing style.

### Step 1 

Using the summary given at the end of each match, I know roughly how my team plays. Shots taken, shots on target, tackles, passes, interceptions are some key stats which will be useful for me to analyse my team.

![Summary](https://github.com/vinothnk/FIFA-23-Stats-Extraction/assets/108440564/44074487-4543-442a-836f-6aa72c3dd04c)

Using python, I tried to use pytesseract to extract out the information given in the picture and clean it. However, I could never get the numbers to appear as pytesseract would only give me the text. I eventually found out about opencv to be able to extract out text and numbers with additional code.

### Code used to extract text and numbers from a picture
thresh = cv2.threshold(image, 0, 255, cv2.THRESH_BINARY_INV + cv2.THRESH_OTSU)[1]
data = pytesseract.image_to_string(thresh, lang='eng',config='--psm 6')

### Step 2
Since I was able to extract out text and numbers, I tried cleaning the data. However, it was tedious as every picture had details which was different from the next. I then stopped and thought about the problem. I realised I only needed certain fields to be extracted out for every picture. 

- Home team name
- Away team name
- Home team score
- Away team score
- Stats of home team
- Stats of away team

I then researched on how to crop pictures by coordinates using python. Using the image package from PIL, I kept a record of the top-left-x, top-left-y and bottom-right-x, bottom-right-y coordinates for each field that I wanted to extract. I then wrote a script to simplify the process which helped a lot to reduce time to extract out the data I wanted.

### Sample Team Name
![home_team_name](https://github.com/vinothnk/FIFA-23-Stats-Extraction/assets/108440564/3a72909f-ca82-41f6-b438-d84923b9d8a3)

### Sample Home Team Stats
![home_team_stats](https://github.com/vinothnk/FIFA-23-Stats-Extraction/assets/108440564/6f11fff0-b2d7-455f-9a18-5c5028b00939)


### Step 3
Once all the information were extracted out into pictures, I once again used pytesseract to extract the data out and put them in a list. There were 17 fields which I required for the team stats. I would count the length of the list to identify if any fields were missing. Then manually check and add or delete if necessary. Once all fields were correct, I would then load it into a DataFrame, which I would then save or append the data into a csv file for analysis at a later period.

![Check_Data Screenshot](https://github.com/vinothnk/FIFA-23-Stats-Extraction/assets/108440564/0084b185-2799-4d95-b60f-dd57564bc40b)

![Data into CSV Sample](https://github.com/vinothnk/FIFA-23-Stats-Extraction/assets/108440564/4bf2954f-274a-4b9b-90e9-83397bb00459)
