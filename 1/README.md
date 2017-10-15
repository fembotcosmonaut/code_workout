
#### Resources:
```bash
sample_output.sh
```

#### Process:
Use the sample_output.sh script to generate the sample text needed for the goals.

#### Goals:

* Produce csv (comma seperated values) output that only has the ID, power, and time. Make sure the "ID:" is not in the output.
```bash
awk '{gsub("ID:", "");print $2, $4, $10}' file.txt | tr ' ' ','
```

* Produce csv output that only has the ID, power, and DAY but only for powers greater than 50.
```bash
cat log.txt | awk '{gsub("ID:", "");print $2, $4, $6}' | awk '$2<50' | tr ' ' ',' | sed 's/.$//'
```

* Produce csv output that only has the ID, power, and time, but only for rows that have double numbers (22, 33, etc...) in the ID field

	Example:
    
		2bc693ae-fbc2-4b0f-b797-5482270bc438,50,06:33:49

```bash
cat log.txt | while read line; do read u p t <<<$(echo $line | awk '{gsub("ID:","");print $2, $4, $10}'); if [[ $( echo $u | egrep '([0-9])\1') != '' ]]; then echo $u $p $t | tr ' ' ','; fi; done
```

