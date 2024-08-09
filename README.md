# Machine-Learning-approach-to-Roommate-Flat-mate-allocation-algorithm-for-BX-students.
A Machine Learning (unsupervised learning) algorithm (leveraging k-means clustering and linear sum assignment optimization) developed for allocating flat mates for the incoming Bachelor of Science students at Ecole Polytechnique using the data extracted from the Roommate (Flat-mate) preferences form that was sent to and filled up by incoming BXs! If you still wonder what the aim of this project, keep reading to understand it in detail!

(**TLDR: Roommate Allocation Algorithm:** This project aims to optimize the allocation of roommates in student housing, ensuring compatibility and adherence to specific constraints. The algorithm uses K-Means clustering and the Linear Sum Assignment method to group students based on their preferences and characteristics.)

## Table of Contents
- [Brief Familiarization](#brief-familiarization)
- [Features](#features)
- [Requirements](#requirements)
- [How the Algorithm/Code Works and What it Does](#how-the-algorithm-or-code-works-and-what-it-does)
- [Installation](#installation)
- [Usage](#usage)
- [Data Preprocessing](#data-preprocessing)
- [Algorithm](#algorithm)
- [Output](#output)
- [Contributing](#contributing)
- [License](#license)

## Brief Familiarization
This section aims to familiarize you (the reader) a bit with the structure of the student housing here at the Bachelor of Science program at Ecole Polytechnique, and also explain the basic constraints etc. You can treat it as a short abstract!

(Please note at some places it might confuse you why it is called a Roommate allocation algorithm when there are individual rooms for the student accomodation:- that is because here we sometimes use the terms appartment/flat interchangeably with room (after the translation from French) so the flatmates get interchanged with roommates!)

### About the student housing: - 
- All the students at the Bachelor of Science program at École Polytechnique are guanrateed a student housing for the entire duration of their studies i.e. 3 years.
- The student housing here takes the form of appartments of the bachelors' beloved Batiment 103 (Residence Bachelor) building.
- Each appartment is composed of 4 indiividual rooms (with attached bathrooms/WC s) and a common area composed of the kitchen, dining areas for everyone and a balcony/hallway alley access door for some appartments.

Now the main **aim** of this algorithm is to allocate 4 (or in some cases 3 since the number of people is not always a perfect multiple of 4!) roommates in a such a way that theuy satisfy the constraints set by the administration and link up people (ofcourse while satisfying the constraints) in such a way that they are compatible with each other in terms of their cleaniness habits, sleep-time schedule, their tendancy towards partying etc (the data which we extract from the room-mates preferences form which we send to the incoming bachelor students). 

### Constraints and general considerations to be followed - 
- The most basic rule is that we can never house the male and female students, there are always male and female only appartments.
- Second rule is that we must have atleast one French national/french speaking individual per room since eventhough we have a fully english taught program, atleast one French speaker per flat/appartment can help every other non-French speaking person in the appartment with the necessary administrative work and things like calling the SPIS (our Emergency heros!) for example who speak mostly only French.
- Another subsidiary/secondary constraint related to the previous constraint is that after the best possible case of 1 French speaker/national per room, we must only have the cases of 2 French speakers/nationals and the worst possible case of 4 French speakers per appartment, since we don't want to isolate the 4 th person out with 3 other French speakers in the case of 3 French speakers per appartment.
- We must try our best to not group the same nationality/language speaking (mostly non-French) people together since mixing up with people from different socio-linguistic backgrounds is a crucial aim of international programmes like ours!
- While using the scoring system (as explained in the brief working of the algorithm!), cleanliness and sleeptime schedules (and the party habits of a person if not detrimental to the results (based on the demographics of the batch/promotion and the data)) should be given the maximum weight since those affect the common area the most and are the most crucial factors which can cause arguments amongst the flatmates (which we must try to avoid!)
- If noise bothers them is an important question and takes a decent weight too.
- And rest everything is taken care of the weighted system of the algorithm.


## Features 
(Basically a short summary of the above).
- Uses student preferences to allocate roommates.
- Ensures that each room has at least one French national.
- Avoids grouping students with the same nationality in the same room.
- Takes into account various student preferences, such as cleanliness, sleep schedules, noise tolerance, etc.

## Requirements
Please note - I uploaded the code in the form of a Jupyter notebook here since it is the best for explaining for what is intended to be done side by side too, so feel free to use that as well, but if you want to use only python you can go ahead with that too!
- Python 3.7 or higher
- Pandas
- NumPy
- Scikit-learn
- Scipy

## How the Algorithm/Code Works and What it Does
So basically this algorithm works on a weighted scoring system (and the approach is that higher the weight of any factor, the higher the chances of people with similiar scores of that factor are likely to end up together - so a grouping together approach) with varied weights for each factor (for eg - cleanliness and sleep-time) while taking into consideration the hard constraints set by the admins which we must adhere to! We use K-means clustering and Linear Sum Assignment (for optimization) to achieve this. In simple terms, K is set to the number of rooms ofcourse which we achieve by dividing the total number of students/4. And for the mapping part in the K - means clustering, we use the lamda function (or operator) of python to map literal.string reponse values to scores like 5, 3 and 1 for the type of response for each question so that we can effectively do the scoring! It may seem wierd that how do the people grouped together based on the constraints and scores are actually compatible matches! Well its all about choosing your weights correctly again depending on the demographics of your promotion/batch and the requirements according to the data you have/requirements you must satisty. While trying to run this algorithm with various datasets, you would realise why and how it works! Also don't forget to clean the data in the dataset (here an excel sheet) to work with this algorithm, and don't forget to plug in the filepath of your excel sheet/.xlsx file at the right place in the code! Please refer the sample data for the same!

### NB - 
Not all the people end up filling up the roommate preference form and leave it completely up to destiny to decide their roommates! This can ruin 2 to 3 or a bit more of the many groups of 3 - 4 people that you would end generating from this algorithm. That invited you to do some hand swapping and hand allocations for the remaining people!

### Please note - 
since this is an unsupervised learning approach whih uses clustering, we need to always check the results we obtained briefly, but the amount of checking and hand swaps (for bad matches made by the algorithm since we have a lot of constraints and an overall score to adhere to) you would need to do using this algorithm would be way less compared to general constraint satisfaction and general scoring algorithms which were in use by the previous promotions here at the BX! 
TLDR - Always check your results before finalising stuff if you are the person in charge!

### Note 2- 
I ioncluded only the 2 important (one final) versions of the algorithm here, but ofcourse I had to play around with it a bit for it to make sense as I kept getting new data and only finaliuzed stuff when I had the maximum data! So, if you want to experiment around with some stuff while contributing to an open source project or whereever the usage of this code is admissable (please refer the #MIT Licencse) please don't hesitate!

## Installation
1. Clone the repository:
    ```sh
    git clone https://github.com/yourusername/roommate-allocation.git
    ```
2. Change to the project directory:
    ```sh
    cd roommate-allocation
    ```
3. Install the required packages:
    ```sh
    pip install pandas numpy scikit-learn scipy
    ```

## Usage
1. Prepare your input data as an Excel file (for eg - `Roomate form BX27 (Responses).xlsx`), ensuring it includes the required columns:
    - Name, Surname
    - Sex
    - Nationality
    - Languages spoken
    - Sleep schedule (weekdays and weekends)
    - Cleanliness
    - Noise tolerance
    - Party person
    - Mind invites
    - Invite people
    - Handle disagreements
    - Sharing habits
    - Clean dishes after use
Also don't forget that if you are using this code as it is, ensure that there are no spaces between commas for multiple answers to certain questions. If you want to clean your data efficiently, don't shy away from writing simple functions or chaing the separation commands in the code!

2. Run the script (if not using a Jupyter notebook!):
    ```python
    python roommate_allocation.py
    ```

## Data Preprocessing
The data preprocessing involves:
- Cleaning and normalizing the input data.
- Mapping categorical and textual responses to numerical values.
- Calculating compatibility scores based on various student characteristics.

## Algorithm
### Data Preprocessing and Feature Mapping
The following steps are performed to preprocess the data and map features:
- Clean and normalize nationality responses.
- Normalize Yes/No responses to lowercase.
- Normalize languages by removing spaces.
- Map the features to numerical values based on student responses.

### Clustering and Compatibility Scoring
The algorithm calculates compatibility scores between students and uses K-Means clustering to group students into clusters. The Linear Sum Assignment method is then used to ensure optimal assignment with specific constraints, such as ensuring at least one French national per room and avoiding grouping the same nationality together.

## Output
The final room assignments are saved to an Excel file (`room_allocation_results_optimized.xlsx`).

## Contributing
Any feedback/suggestions is both welcome and appreciated. Please email me at - <Jaianshofficial26@gmail.com>

## License
This project is licensed under the MIT License (see [LICENSE](https://github.com/JaiAnshSB26/Mentor-Mentee-Allocation-Algorithm/blob/main/LICENSE)).

