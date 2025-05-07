# CSC3170-LLM-DB-school
Combining large language models with the school personnel management database is mainly aimed at enhancing management efficiency, optimizing the decision - making process, and providing more intelligent services. Our model mainly based on on the use of ChatGPT-3, which has powerful language processing capabilities and a low API call cost.

## Acknowledgments

We would like to extend our sincere gratitude to [gbasin](https://github.com/gbasin) and all the contributors of the [LLM - DB](https://github.com/gbasin/LLM-DB) project. Our project is inspired by and references the code from their repository. Their excellent work and dedication to open - source have provided us with a valuable starting point and a wealth of inspiration.

The open - source spirit demonstrated by the [LLM - DB](https://github.com/gbasin/LLM-DB) project has not only accelerated the development process of our project but also enhanced the overall quality of our code. We believe that the open - source community is a powerful force for innovation, and we are honored to be part of this ecosystem.

If you are interested in learning more about the original project, please visit [LLM - DB](https://github.com/gbasin/LLM-DB) on GitHub.

## abstract
We use historical data to enable the model to respond and execute operations quickly. Here are examples of four basic operations: insert, delete, query, and update. LLM only provides SQL statements, and delete and update operations will go through three rounds of review to prevent incorrect operations from causing detrimental chain reactions in the database.

## insert
```
python src/main.py "add a student whose name is John from the class of 2027 belongs to SHAW college, he will select SDS.His phone number is 18718927911."

INSERT INTO Student (
    StudentID, Name, E-mail, Gender, Year, Major, GPA, School, College, `Tuition fees`, Scholarships, `Financial Aids`, `Honors and Rewards`, Nation, `Phone Numbers`, `Mailing Address`, `Emergency Contact`, `Graduate Status`
)
VALUES (
    NULL, 'John', 'none', 'none', 2027, 'SDS', 'none', 'none', 'SHAW', 'none', 'none', 'none', 'none', 'none', '18718927911', 'none', 'none', 'none'
);
```

## delete
```
% python src/main.py 'I need to delete the information of a student named John who dropped out in the class of 2021. He is French, his GPA is 1.5, his student ID is 125090833, and his major is data science.'

DELETE FROM Student 
WHERE StudentID = 125090833 
  AND Name = 'John' 
  AND Year = 2021 
  AND Nation = 'France' 
  AND GPA = 1.5 
  AND Major = 'data science';

```

## query
```
% python src/main.py 'Please help me find the email addresses of the students who are taking Linear Algebra taught by Tom Willson in the spring semester of 2025. The students should be in their sophomore or junior year. Summarize the list of email addresses to help the Academic Affairs Office send out a questionnaire'

SELECT s.`E-mail`
FROM 
    Student 
JOIN Course c ON s.Year = c.Year
JOIN Professor p ON c.Instructor = p.InstructorID
WHERE 
    c.Year = 2024 
    AND c.Schedule LIKE '%Spring%' 
    AND c.`Course Name` = 'Linear Algebra' 
    AND p.Name = 'Tom Willson'
    AND (s.Year = 2 OR s.Year = 3); 
```

## update
```
% python src/main.py 'I need to help a student change their major and the corresponding college. Here is the information of the student John from the class of 2021: He is French, with a GPA of 1.5, and his student ID is 125090833. His current major is data science. He will switch to FE, and his college will also change from SDS to SME.'

UPDATE Student
SET Major = 'FE',
    College = 'SME'
WHERE StudentID = 125090833
  AND Name = 'John'
  AND Year = 2021
  AND Nation = 'France'
  AND GPA = 1.5
  AND Major = 'data science';
```
