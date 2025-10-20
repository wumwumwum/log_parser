# log_parser
Parse and create a summary file of Windows Event Log/ syslog file (Python)

Simple Project #2
To force myself into familiarity with scripting, I wanted to try some simple scripts that have practical use.
The goal was to create a sciprt that would parse and summarize sys log files. This would provide a count of event levels/ groups.

Steps:
1.) I ensured that Python 3 was installed (it was) and verified the version (python 3.13)

2.) I opened a cmd (admin) and installed dependencies using:

	pip install regex

3.) I created a copy of the Windows Event Log from "C:\Windows\System32\winevt\Logs\Application.evtx" and exported the log to "system.log.txt". 

4.) I verified that the file was created.

5.) I created a script by opening Notepad++ and creating a file called "log_parser.py" 

6.) I opened the log_parser.py file in Notepad++ and wrote the following:

	import re, collections

	log_file = "system.log"
	report_file = "log_summary.txt"

	pattern = re.compile(r"ERROR|WARNING|INFO")
	counts = collections.Counter()

	with open(log_file) as f:
    	for line in f:
        	match = pattern.search(line)
        	if match:
           		counts[match.group()] += 1

	# Print to console
	print("Summary of log levels:")
	for level, count in counts.items():
    	print(f"{level}: {count}")

	# Save to text file
	with open(report_file, "w") as out:
    	out.write("Summary of log levels:\n")
    	for level, count in counts.items():
        	out.write(f"{level}: {count}\n")

	print(f"\nReport saved as {report_file}")


7.) Testing. Ran py file test functionality. In cmd,:

	python log_parser.py

8.) Opened file "log_summary.txt" located in same directory as py script. Output:

	Summary of log levels:
	INFO: 1

