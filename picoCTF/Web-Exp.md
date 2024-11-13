# SOAP


# Forbidden Paths

**Flag:** `picoCTF{7h3_p47h_70_5ucc355_6db46514}`

**Solution:**
- The main hint in the challenge was the fact that the website was filtering *absolute* file paths. 
- I noticed the .txt files listed on the website given. http://saturn.picoctf.net:<port\>.
- ![forbidden paths](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/picoCTF/images/webex1.JPG?raw=true)
- By using the knowledge of absolute vs relative paths, I remembered relative paths don't start with a `/`(root directory), and that other directories in the path can be represented by `../` .
- To get the file, I entered `../../../../flag.txt` as the description said the file was in `/usr/share/nginx/html/`.


**Concepts learnt:**
1.  I recalled the use of `..` to symbolise parent directory.

**Mistakes & other approaches:**
- First, I tried editing the URL directly with the path provided and it didn't work. 
- I also tried entering the given files names on the home page, but they seemed to be not be found

# Cookies



