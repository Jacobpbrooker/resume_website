---
layout: post
title:  "Fitness Program Generator in C++"
date:   2021-10-07 15:43:03 -0400
categories: jekyll update
post_description: This is a program made to create a custom fitness program, includes specific muscle targets and avoidance. This program was written using Object Oriented C++.
---
With the rise of COVID, one of the lifestyle changes I miss the most was heading to the gym for a workout. While waiting patiently for the return to normalcy, I decided to make an application that would create a weekly workout routine based on certain muscle selections. 

The main reason to complete this project was to practice Object Oriented programming. Specific techniques I wanted to apply during the development were working with enums, working with vector class templates, and data loading from a csv. 

<h3>Application Decomposition and Explanation</h3>

First, I set myself a challenge to use enumerated classes as a core data type. I set each of the muscle groups, difficulty, movement, equipment, and targeted aread to an enum class. This allowed me to load the data from a string and use an extremely fast case comparison to return the enum.

~~~c++
enum class muscleGroup {NONE, AbdominalsLower, AbdominalsObliques, AbdominalsTotal, AbdominalsUpper, BackLatissimusDorsi, BackLatDorsiRhomboids, Biceps, CalvesGastrocnemius, CalvesSoleus, ChestPectoralis, LegsHamstrings, LegsQuadriceps, LowerBackErectorSpinae, ShouldersDeltsTraps, ShouldersRotatorCuff, Triceps};
enum class intensity {NONE, EASY, MEDIUM, HARD };
enum class PP { NONE, PUSH, PULL};
enum class modality { NONE, FREEWEIGHT, MACHINE, CABLES, BODYWEIGHT};
enum class joint { NONE, COMPOUND, ISOLATION};
~~~
The next code technical aspect I set out to accomplish while developing this project is to use a vector list as the containers to hold the exercises. I used a vector of exercises that pertained to one specific muscle group, and then created a vector of vectors where all exercises could be stored.

~~~c++
class weeklyProgram {
	vector <exercise> weeklyExercises;
public:
	void makeProgram(excerciseList, vector<muscleGroup>);
	void displayProgram();
};

~~~

The last code block I would like to demonstrate is how the the exercises are loaded into the application through a csv file. Essentially, every line is loaded into from the csv and the comma's are used to determine location of different data sections. As the csv contents are loading in as a string, I needed to use a string to enum to convert the data to be usable by the exercise object. The exercise object is given all the data as arguments and the object is created. Finally, a switch case is used to determine which vector the exercise will be attached too.

~~~c++
void excerciseList::loadExcercises(string fileName)
{
	fstream fin;
	fin.open(fileName);

	if (fin.is_open())
	{
		while (!fin.eof())														// do work here creating objects in loop and pushing to vector list
		{
			string line;
			getline(fin, line);													// get the entire line and then will need to parse data to create the objects needed

			istringstream issLine(line);
			string muscleGRP;
			string exc;
			string lvl;
			string pushp;
			string modi;
			string jnt;
									
			getline(issLine, muscleGRP, ',');									// parse the data and covert to enum class values
			getline(issLine, exc, ',');
			getline(issLine, lvl, ',');
			getline(issLine, pushp, ',');
			getline(issLine, modi, ',');
			getline(issLine, jnt);

			muscleGroup m_grp = stringToMuscleGroup(muscleGRP);					
			intensity i_ty = stringToIntensity(lvl);
			PP p_p = stringToPushPull(pushp);
			modality m_ty = stringToModality(modi);
			joint j_nt = stringToJoint(jnt);
									
			excercise excer(m_grp, exc, "N/A", i_ty, p_p, m_ty, j_nt, ++excerciseCounter);  // create the excercise object 
			
			switch (excer.getMuscles())
			{
			case muscleGroup::NONE:
				this->NONE.push_back(excer);
				break;
			case muscleGroup::AbdominalsLower:
				this->AbLow.push_back(excer);
				break;
			case muscleGroup::AbdominalsObliques:
				this->AbObl.push_back(excer);
				break;
			case muscleGroup::AbdominalsTotal:
				this->AbTot.push_back(excer);
				break;
			case muscleGroup::AbdominalsUpper:
				this->AbUpp.push_back(excer);
				break;
			case muscleGroup::BackLatissimusDorsi:
				this->BackLatDor.push_back(excer);
				break;
			case muscleGroup::BackLatDorsiRhomboids:
				this->BackLatRhom.push_back(excer);
				break;
			case muscleGroup::Biceps:
				this->Bic.push_back(excer);
				break;
			case muscleGroup::CalvesGastrocnemius:
				this->CalGas.push_back(excer);
				break;
			case muscleGroup::CalvesSoleus:
				this->CalSol.push_back(excer);
				break;
			case muscleGroup::ChestPectoralis:
				this->ChestPec.push_back(excer);
				break;
			case muscleGroup::LegsHamstrings:
				this->LegHam.push_back(excer);
				break;
			case muscleGroup::LegsQuadriceps:
				this->LegQuad.push_back(excer);
				break;
			case muscleGroup::LowerBackErectorSpinae:
				this->LowBack.push_back(excer);
				break;
			case muscleGroup::ShouldersDeltsTraps:
				this->ShouldDelt.push_back(excer);
				break;
			case muscleGroup::ShouldersRotatorCuff:
				this->ShouldRot.push_back(excer);
				break;
			case muscleGroup::Triceps:
				this->Tric.push_back(excer);
				break;
			}
		}
	}
	else
		cout << "Failed to open file - " << fileName << endl;
}
~~~

<h3>Running the Application</h3>
First, the main menu of selection is displayed to the console.
<br><br>
<img src="{{site.url}}{{ site.baseurl }}/assets/img/fitnessmain.PNG" height="300px">
<br><br>
Next, the user makes a selection of the muscle group, and the amount of exercises they would like of that muscle group.<br>
<img src="{{site.url}}{{ site.baseurl }}/assets/img/fitnessselection1.PNG" height="300px">
<br><br>
Another user selection, this time with more than one exercise requested.
<img src="{{site.url}}{{ site.baseurl }}/assets/img/fitnessselection2.PNG" height="300px">
<br><br>
Lastly, the program is exited, and the user is presented with a custom exercise program!
<img src="{{site.url}}{{ site.baseurl }}/assets/img/fitnessresults.PNG" height="300px">
<br><br>
<hr>

<h3><a href="https://github.com/Jacobpbrooker/fitnessProgramPlanner">You can find the GitHub Repo here!</a></h3>
<br>
If you have any questions at all, please do not hesitate to reach out. Thanks for reading!