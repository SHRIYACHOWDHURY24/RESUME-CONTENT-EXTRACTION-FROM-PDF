# RESUME-CONTENT-EXTRACTION-FROM-PDF
The project implements a multi-step algorithm to accurately extract structured information from resumes, focusing on key sections such as Personal Data, Contact Information, Professional Summary, Experience, Education, Skills, and Certifications.
Key Features:
Extracts essential resume data: Captures personal details, professional summaries, work experience, educational qualifications, skills, and certifications.
Handles unstructured text: Cleans and structures data from messy, unstructured PDF documents.
Flexible email extraction: Corrects email addresses with extra prefixes or formatting issues.
Technologies, Libraries, and Algorithms Used:
Technologies:
Python: Core programming language used for the entire project.
PyPDF2: Used for extracting text from PDF files.
spaCy: A Natural Language Processing (NLP) library used for identifying and extracting named entities such as person names.
Libraries:
PyPDF2: For extracting and reading the textual content of PDFs.
spaCy: For NLP tasks like recognizing named entities (e.g., names, locations) from unstructured text.
re (regex): For pattern matching, especially for extracting email addresses, phone numbers, and other structured data.
json: For saving the extracted structured data in a JSON format.
Algorithms:
Regular Expressions (regex): Used extensively for extracting specific patterns like emails, phone numbers, and section headers from the raw text.
NLP Techniques: Leveraged spaCy’s entity recognition to identify and extract the name and potentially other structured data from the PDF.
PDF Text Extraction: Using PyPDF2 to handle the variability of text layout in PDF files.
1. Text Extraction:
Input: A resume in PDF format.
Process:
The PyPDF2 library is used to extract raw text from the PDF. This library reads the PDF file and extracts its textual content while handling multiple pages.
The extracted text is processed as a continuous string.
Output: A raw text string that contains all the information from the PDF.
2. Section Detection and Classification:
Goal: Identify and classify different sections of the resume such as Professional Summary, Experience, Education, etc.
Process:
The text is split into lines, and a series of keywords like "Profile", "Professional Summary", "Experience", "Education", etc., are used to detect when a new section begins.
For each section, a custom function is applied to extract the relevant data.
3. Extracting Personal Data:
Process:
Name: spaCy’s Named Entity Recognition (NER) is used to detect a person’s name from the first few lines of the resume. The assumption is that the name appears at the top, and spaCy is able to classify "PERSON" entities.
Email: A regular expression ([a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}) is used to capture valid email patterns, ensuring only valid emails are extracted even if there are extra words or characters.
Phone Number: Another regex pattern (\+?\d[\d -]{8,12}\d) is used to detect phone numbers, accommodating various formats such as international codes.
Output: Structured data with fields for Name, Email, and Phone Number.
4. Professional Summary Extraction:
Process:
The algorithm searches for keywords like "Profile" or "Professional Summary" in the extracted text and starts recording the content until it encounters another section heading like "Experience" or "Education."
It concatenates the text lines between these boundaries to form a coherent summary.
Output: A string that represents the professional summary of the candidate.
5. Experience Extraction:
Process:
Keywords like "Experience" or "Work History" are used to identify the start of this section.
The function collects job titles, company names, and dates by identifying lines that match patterns like "2023/07 – 2023/08" (date ranges) or typical job title formats.
Output: A list of work experiences, where each entry contains a title, company, location, and dates.
6. Education Extraction:
Process:
The algorithm detects common educational degrees like "B.Tech", "M.Sc", "PhD", etc., by scanning for typical degree names.
It also captures other information such as the institution's name, CGPA/grades, and the year of graduation.
Output: A list of educational qualifications (degree, institution, year, and grade if available).
7. Skills Extraction:
Process:
A predefined list of common skills (e.g., "Python", "Machine Learning", "Java", "SQL") is used to scan the text and extract technical skills mentioned by the candidate.
The function looks for these skills anywhere in the document, typically in a dedicated "Skills" section.
Output: A list of extracted skills.
8. Certifications Extraction:
Process:
Keywords like "Certification", "Certified", "Certificate" are used to detect this section.
The function captures any line that matches these keywords, removing any irrelevant or adjacent text.
Output: A list of certifications achieved by the candidate.
9. Data Post-processing:
Process:
After each section is extracted, post-processing ensures data cleanliness:
Emails: Remove any non-email text that may appear before or after the email.
Experience: Check for consistency in dates and job titles.
Summary: Concatenate broken lines to ensure readability.
10. Final Output:
The output is structured data in the form of a Python dictionary or JSON object, containing the extracted information under specific keys such as PersonalData, Experience, Education, Skills, and Certifications.
