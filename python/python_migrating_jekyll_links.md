# Migrating Wordpress links to Jekyll

Migrating Wordpress posts to Jekyll is a huge pain, even with [this helpful extension](https://github.com/benbalter/wordpress-to-jekyll-exporter).

The links to posts remain pointed to the old blog. Here's a Python script that converts them in-place. If you're moving
to Jekyll on GitPages, check where the images actually upload by uploading them first. 

```python
import re
import os

print os.getcwd()

old_url = 'wordpressblogurl'
new_url = 'githubpagesurl'  #check which dir the images point to

for f in os.listdir(os.getcwd()):
     if f.endswith(".md"):        
        md_file_in = open(f, "r")
        md_file_out = open("%s_o.md"% f, "w+") 
        for line in md_file_in:
            if old_url in line:
                new_line = re.sub(old_url,new_url,line)
                md_file_out.write(new_line)
            else: md_file_out.write(line)
            
            

# add suffix to converted docs
suffix = "_o.md"

#remove suffix to rename them to original files
for f in os.listdir(os.getcwd()): 
    if f.endswith("_o.md"): 
        os.rename(f, f.replace(suffix,'',1))  ```
