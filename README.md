# Iterative-zI


## Overview

The identification of emergent structures in complex dynamical systems is a very difficult task with broad applications. In particular, the formation of intermediate-level dynamical structures could allow a high-level description of the organization of the system itself, and thus to its better understanding.
We here present a method based on the Relevance Index method aimed at revealing these dynamical structures (Relevant Sets, or RSs in the following).
The method involves two basic steps: (i) the detection of the candidate RSs based on the computation of the Relevance Index, and (ii) the iterated application of a process composed by a sieving action followed by the merger of the grouped variables and a new candidate RSs detection, till reaching the final grouping (composed by the “real” RSs).

The reference papers in which the details of the method are presented are:

Villani, M., Sani, L., Pecori, R., Amoretti, M., Roli, A., Mordonini, M., Serra R., Cagnoni, S. An iterative information-theoretic approach to the detection of structures in complex systems. Complexity 2018

D’Addese G., Sani L., La Rocca L., Serra R., Villani M. Asymptotic Information-Theoretic Detection of Dynamical Organization in Complex Systems Entropy 2021, 23(4), 398

The script takes as input:

	- discretized matrix representing the data set, composed of N variables (the columns) and M observations (the rows) 
	
and give as output:

	- file containing the succession of groupings, up to the definitive solution (the document’s last line)
	- list of folders showing the data set used in each iteration (file.txt) and the corresponding evaluation of the subsets taken into consideration (grind.txt)


The code is optimized for Python versions 3.6 or higher

## Input
The script can take in input more files at a time. Create a folder called ``files`` to fill with all the text files that you want to analyze.

The input files must be generated as follows:

	- first line containing the sistem element names separated by tabulation. Element names must not contain spaces or "_" (used to divide the relevant set). All the name must be unique

	- other line containing the elements expression values ​​(discretized). The order of the lines is not important. The values ​​on the row must appear in the same order as the elements in the first row.

see ``example.txt`` as an example

## Preprocessing

Before starting with the main script it is required a preprocessing step.
```
"python3 deleter.py"
```
This script searches and eliminates all the columns of the input matrix where value remains constant for the whole column. This type of element does not carry information and could be included in any of the groups: it is therefore better that it be eliminated. IMPORTANT NOTE: this script will overwrite the starting file in the directory files.

After this first step is possible to proceed with the execution of the main script. Type on the command line:

"python3 run.py"

## Parameter
The program supports the following options

	``-g --gruop`` takes as input an integer which is used to set the maximum size of the subsets to be analyzed. The default value is 3.

	``-z --zi`` takes in a float that is used to set the zI threshold  used to stop  the iterative merge. The default value is 3.

Example:
```
"python3 run.py -g 4 -z 2.7"
```
Once the run is complete, a folder will be created for each file in input, containing the script output.

## Output
the output is defined as follows:

	- Directory ``results``: Each iteration is stored in a dedicated folder, identified by the iteration number. Inside the folder there are two files:

		• ``file.txt``: the state of the system before the merge of the current iteration.

		• ``grind.txt``: a list of all the groups analyzed and the value of the zI calculated on them. the order of the gruop is defined by zI, sorted in descending order. This type of information is useful for taking a closer look at how the system is organized. However, in many cases it could happen that the file is very large: in this case, creating it at each iteration can involve a high consumption of disk space. This problem can be circumvented by printing only the first 1000 most relevant groups. This value can be increased or decreased at will in the ``cacolate_zI.py`` file by changing the value of the variable at the beginning of the file ``num_line_to_print``.

	- ``sequence.txt``: the sequence of RSs groupings at each iteration. The second-last element of each row is the the join carried out in that iteration, followed by zI value assigned to it. the last line of this file represents the last merge that was possible using the threshold provided in input. This line then represents the relevant sets of the system. In each line the relevant sets are separated by tabs. The elements that form each RS are separated by the character "_"

