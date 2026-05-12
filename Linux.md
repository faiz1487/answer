sed -n '20,30p' app.log  ---------------print the line no 20 to 30 from app.log
sed -i '20,30d' app.log ----------------Delete the line no 20 to 30 from app.log
sed -n '/INFO/p' app.log  --------------Print INFO from this app.log
sed 's/INFO/LOG/g' app.log -------------Replace where INFO equal to LOG
sed -n -e '/INFO/=' app.log ---------Print the line no. where INFO present
sed -n -e '/INFO/=' -e '/INFO/p' app.log-----Preint INFO with line no.
sed '1,15 s/INFO/LOG/g' app.log -----------Print LOG in place of INFO from line 1 to 15 but show all log in this file
sed '1,15 s/INFO/LOG/g; 1,15p; 16q' app.log ----------Print LOG in place of INFO from line 1 to 15 only
where -n for filter out the pattern from the file, -e for experission(=) use, = -for print the line no.
gerp -i INFO app.log ----------------print INFO from app.log
awk '{print $1,$2,$3}' app.log ---------print the column 1,2,3
awk '/info/ {print $1,$2,$3}' app.log       ----------------- print the info coloumn 1,2,3
awk '/info/ {print $1,$2,$3}' app.log > only_info.log  ----------create seperate file of info
awk '/info/ {count++} END {print count}' app.log  --------it count the no. of info in this file
awk '{print $2}' app.log ------------------- print coloumn 2
awk '$2 >= "08:53:00" && $2 <= "08:53:59" {print $2,$3,$4}' app.log  -------print only particular range
AWK 'NR >= 2 && NR <= 10 {print NR}' app.log -------print row from 2 to 10
<p style="color:red;">awk '/info/ {count++} END {print count}' app.log  --------it count the no. of info in this file</p>
<p style="color:red;">grep -i -c info app.log --------------------it count the no. of info in this file</p>
<p style="color:red;">This text is red</p>
