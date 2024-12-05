# PBI2. Display the background, title, date and time on the screen

## Purpose (目的)

The user can recognize the line name and the date and time displayed on the screen.

## Requirements (要件(やりたいこと))

- The system should display the line name at the top left and the date and time at the top right.  
  GPS ミリ波 1 号ライン
- The date and time must be displayed in YYYY/MM/DD HH: MM: SS format and can be updated in real time.
- Develop according to TDD.
- Push the results to Git.
- Use the following for the Unit test environment
  - Javascript / Vue.js: Jest
  - Python / Flask: Pytest
- Nihongo Sentences Reference File:
  [Andon*System*-_NihongoText_Revised_error_code\_\_3_.xlsx](/uploads/18c5d9d93376bb035642eedba975ded5/Andon_System_-_NihongoText_Revised_error_code__3_.xlsx)

![S1_PBI2](/uploads/ee11f475b74cbf358a9c11902ebcd3b6/S1_PBI2.png)

<hr>

# PBI3. Display image of operation information for each process

## Requirements (要件(やりたいこと))

- Display operation information for each process.
- Load the image file \
  Line Chart: \
  ![S1_PBI3_1](/uploads/900653313284da8c1727df4abbe6e931/S1_PBI3_1.png) \
  Display the yellow green line on the left side of the screen \
  Label: 稼働状況, 稼働中
  ![S1_PBI3_2](/uploads/adba9fbfec788a35a6ad2c94d0584125/S1_PBI3_2.png)
- The green and red squares that appear above the yellow-green lines should read the coordinates specified by the coordinates taken from the DB \
  ![S1_PBI3_3](/uploads/2b7971de2874075e62fbe01397ef277d/S1_PBI3_3.png)
- Please do not use japanese numbered list format: ①②③...
- Develop according to TDD.
- Push the results to Git.
- Use the following for the Unit Test environment
  - Javascript / Vue.js: Jest
  - Python / Flask: Pytest
- Create Necessary Diagrams: Component Diagram, ERD Diagram, Dataset Diagram and Class Diagram
- Apply JSDoc and Docstring in code for documentation

<hr>

# PBI4. Operating Status Indicator

## Requirements (要件(やりたいこと))

- Change the color of each process according to the operating status. \
  ![S1_PBI4](/uploads/601be6c98342d818ae8fa3425da9d222/S1_PBI4.png)
- If the operation status is Abnormal occurrence (異常発生中), please change the background color to red.
- If the operation status is up and running (稼働中), please change the background color to green.
- If the operation status is During preparation (準備中), please change the background color to yellow.
- Develop according to TDD.
- Push the results to Git.
- Use the following for the Unit Test environment
  - Javascript / Vue.js: Jest
  - Python / Flask: Pytest
- Create Necessary Diagrams: Component Diagram, ERD Diagram, Dataset Diagram and Class Diagram
- Apply JSDoc and Docstring in code for documentation

<hr>

# PBI5. Operation Process Feature

## Requirements (要件(やりたいこと))

- Change the color of each process according to the operating status.
- Obtain the operation status from the last process. In the same way, change the color according to the operating status.
- If the operation status is Abnormal occurrence (異常発生中), please change the background color to red.
- If the operation status is up and running (稼働中), please change the background color to green.
- If the operation status is During preparation (準備中), please change the background color to yellow.
- Develop according to TDD.
- Push the results to Git.
- Use the following for the Unit Test environment
  - Javascript / Vue.js: Jest
  - Python / Flask: Pytest
- Create Necessary Diagrams: Component Diagram, ERD Diagram, Dataset Diagram and Class Diagram
- Apply JSDoc and Docstring in code for documentation
