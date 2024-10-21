+-+-+-+-+-+-+-+ +-+-+-+-+-+-+-+-+-+ +-+-+-+-+                      
|L|e|x|i|c|a|l| |D|e|c|i|s|i|o|n|s| |T|a|s|k|                      
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+ +-+-+ +-+-+-+-+-+-+-+
|B|e|k| |N|.|I|.| |H|a|r|d|y|,| |D|w|i|g|h|t| |J|.| |K|r|a|v|i|t|z|
+-+-+-+-+-+-+-+-+ +-+-+-+-+-+-+ +-+-+-+-+-+-+ +-+-+ +-+-+-+-+-+-+-+
|(|2|0|2|4|)|                                                      
+-+-+-+-+-+-+                                                      

  _   _   _   _   _   _   _   _  
 / \ / \ / \ / \ / \ / \ / \ / \ 
( O | v | e | r | v | i | e | w )
 \_/ \_/ \_/ \_/ \_/ \_/ \_/ \_/ 

This folder contains the script for a Lexical Decisions Task using jsPsych version 7.
There is a total of 72 pairs, or 144 individual words/trials
There are 8 possible conditions for a single pair of words to appear in. They are:
EVALUATED - SUP->SUB (Superordinate -> Subordinate word) - COLOR->BLUE
EVALUATED - SUB->SUP (Subordinate -> Superordinate word) - BLUE->COLOR
CONTROL - PSUP->SUB (Pseudosuperordinate -> Subordinate word) - ORLOC->BLUE
CONTROL - SUP->PSUB (Superordinate -> Pseudosubordinate word) - COLOR->UBLE
CONTROL - SUB->PSUP (Subordinate -> Pseudosuperordinate) - BLUE->ORLOC
CONTROL - PSUB->SUP (Pseudosubordinate -> Superordinate) - UBLE->COLOR
CONTROL - PSUP->PSUB (Pseudosuperordinate -> Pseudosubordinate) - ORLOC->UBLE
CONTROL - PSUB->PSUP (Pseudosubordinate -> Pseudosuperordinate) - UBLE->ORLOC
A single pair can appear in 72 possible orders, but only in one condition per participant. 
Therefore, this is a fully counterbalanced set of the 576 possible orders. 

There are 12 catch trials, intended to catch bots and AI.
These catch trials are words or pseudowords as images. A bot or artificial should perform at chance with these trials.
2 catch trials are presented in the practice trials.
10 catch trials are presented in the experimental trials.
Catch trials never interrupt a pair.

  _   _   _   _   _   _   _  
 / \ / \ / \ / \ / \ / \ / \ 
( j | s | P | s | y | c | h )
 \_/ \_/ \_/ \_/ \_/ \_/ \_/ 
 As stated previously, this experiment uses the 7th version of jsPsych.
 It uses the:
 jsPsych library (jspsych.js)
 jsPsych button reponse plugin (plugin-html-button-response.js)
 jsPsych keyboard response plugin (plugin-html-keyboard-response.js)
 jsPsych preload plugin (plugin-preload.js)
 and the jsPsych survey plugins (plugin-survey-html-form.js, plugin-survey.js)
 The jsPsych same-different plugin (plugin-same-different-html.js) is an artifact from an earlier version of this experiment and is not used.
 But I am a little too nervous to delete it. I don't know why.  
 The fact that you're reading this at all is shocking to me. 

 I am however incredibly thankful to the core team of jsPsych, who have definitvely saved my grad school career.
 They are Josh de Leeuw of Vassar College, Becky Gilbert of MIT, and Björn Luchterhandt of Paderborn University. 

  _   _   _   _     _   _   _   _   _   _   _   _  
 / \ / \ / \ / \   / \ / \ / \ / \ / \ / \ / \ / \ 
( d | a | t | a ) ( c | l | e | a | n | i | n | g )
 \_/ \_/ \_/ \_/   \_/ \_/ \_/ \_/ \_/ \_/ \_/ \_/ 

 This section is referencing non-experimental documentation/DataCleaningAndRenaming102124.ipynb.
 
 As I completely forgot to comment what each section of the notebook does, on the NOTEBOOK itself, here is that information.

 Section I:
 This one, courtesy of my short term memory loss, receives a label.
 This script renames the files located within each Order#{letter}/data file, as they will instead have
 a randomly generated session number. They usually look something like session-18310291240
 This script renames it, really just for ease. There are technically other ways to do this entire logic, but this is by far the easiest.

Section II:
This section takes those messy session files and turns them into easy to read CSVs, stripped down to the most important (and relevant) information.
It also outputs the catch trials to a seperate folder for later exclusion.

Section III:
This section searches for two types of catch image trial csvs. Those options are those without capital Bs, and those with capital Bs.
Capital Bs represent a file where the keypresses were reversed. Or if you're a fan of "m meaning real word and z meaning pseudoword", represent the standard files.
File names without capital Bs represent a file where keypresses are standard. Or again, if you're a fan of the statement mentioned previously, represent the reversed files.
It then uses this simple answer key to determine whether participants have passed the first order exclusion criteria:
Are you a bot?

Section IV:
Assuming someone has passed the previous section and has not been removed for further analysis, we must now determine accuracy.
This section goes through the produced CSVs from Section II, and locates their correct responses. 
And, if there is a capital B in the file name, it reverses the correct answer. 
Now, we have our final CSVs to work with for analysis. 

Section V:
We are now going to determine the 2nd order exclusion criteria. Have participants hit 80% accuracy?
This is not across trial pairs, even though trial pairs where at least one response was incorrect will be excluded from analysis.
This is an overall determination to know if we have to replace the participant.

  _   _   _   _   _   _   _   _     _   _   _   _   _   _   _  
 / \ / \ / \ / \ / \ / \ / \ / \   / \ / \ / \ / \ / \ / \ / \ 
( r | e | n | a | m | i | n | g ) ( o | u | t | p | u | t | s )
 \_/ \_/ \_/ \_/ \_/ \_/ \_/ \_/   \_/ \_/ \_/ \_/ \_/ \_/ \_/ 

 Don't like all the work I just did? 
 Just use non-experimental documentation/RenamingScript.ipynb. Just rename the outputs and figure it out yourself. 

  _   _   _   _   _  
 / \ / \ / \ / \ / \ 
( S | p | a | C | y )
 \_/ \_/ \_/ \_/ \_/ 

This is in reference to non-experimental documentation/SpacySimNeigh.ipynb. 

This notebook provides all of the methodology for how we determined semantic similarity and semantic neighborhood density.

Once we found the nearest 50 neighbors that would not be excluded, we determined the similarity scores by creating a matrix.
We then found the mean and standard deviation of these similarity scores.
This gave us our overall semantic neighborhood density for each word. 
This can be found in non-experimental documentation/semantic neighborhood data/SemanticNeighborhood data.xlsx 
You can find each words list of neighbors at non-experimental documentation/semantic neighborhood data/sub and non-experimental documentation/semantic neighborhood data/sup

  _   _   _   _   _  
 / \ / \ / \ / \ / \ 
( U | s | a | g | e )
 \_/ \_/ \_/ \_/ \_/ 

 Pop this baby right on an AWS server (of course, run all of your necessary installation steps), and post them links to Prolific.
 You can change the words that are presented easily by simply changing them in the javascript files located at order#{letter}/order#{letter}_script.js. 
 Similarly, to change the order, just reorder the timeline found in order#{letter}/order#{letter}.html

  _   _   _   _   _  
 / \ / \ / \ / \ / \ 
( o | t | h | e | r )
 \_/ \_/ \_/ \_/ \_/ 

 Similarly to the same-different plugin, the NOTICEME numbers file (NOTICEME.numbers) contains no useful information.
 It is not used at all within this experiment, and literally contains 0 relevant information, but once again, I am too nervous to delete it and have nowhere else to put it.
 I believe at some point it only existed so I wouldn't lose some important piece of information that I've never lost. 

 Similar documents which only exist due to anxiety are setup.csv and default.js. 

 You can also see remnants of previous catch trial methods in SAMPLE.png, tutorial1.png, and tutorial2.png.

  _   _   _   _   _   _   _  
 / \ / \ / \ / \ / \ / \ / \ 
( c | o | n | t | a | c | t )
 \_/ \_/ \_/ \_/ \_/ \_/ \_/ 

If you've made it this far and have questions, or you want to hear me ramble on some more, you can contact me via 
Github @bekhardy or 
Email rebekahhardy@gwu.edu