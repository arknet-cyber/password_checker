# password_checker by ArkNet

This code is a Python script that checks if a given password has been leaked or compromised in any known data breaches. It uses the Pwned Passwords API to securely retrieve information about leaked passwords.

Let's go through the code step by step:

Imports:

import requests: This is a popular library in Python for making HTTP requests to APIs.
import hashlib: This library provides various hashing algorithms, in this case, it's used to hash the password.
import sys: This module provides access to some variables used or maintained by the interpreter and to functions that interact with the interpreter.
request_api_data(query_char) function:

This function takes a query character as input.
It constructs the URL for the Pwned Passwords API by appending the query character to the base URL.
It makes a GET request to the API and stores the response in the variable res.
If the response status code is not 200 (indicating a successful request), it raises a RuntimeError with an error message.
Finally, it returns the response.
get_password_leaks_count(hashes, hash_to_check) function:

This function takes two arguments - hashes (the response from the API) and hash_to_check (the password hash to search for).
It splits the response text into lines and then splits each line into a tuple of hash and count using the ':' character as the separator.
It iterates over each hash and count pair.
If it finds a hash that matches the hash_to_check, it returns the count.
If no match is found, it returns 0.
pwned_api_check(password) function:

This function takes a password as input.
It hashes the password using the SHA-1 algorithm and converts it to uppercase hexadecimal format.
It splits the hashed password into two parts - the first 5 characters and the rest.
It calls the request_api_data() function with the first 5 characters to get the API response.
It returns the result of calling the get_password_leaks_count() function with the response and the rest of the hashed password.
main(args) function:

This function is the entry point of the script and takes a list of passwords as input.
It iterates over each password in the list.
For each password, it calls the pwned_api_check() function to check if it has been leaked.
If the count of leaks is non-zero, it prints a message indicating how many times the password was found and suggests changing it.
If the count is zero, it prints a message indicating that the password was not found.
Finally, it returns 'done!'.
if __name__ == '__main__': block:

This block of code ensures that the main() function is only executed if the script is run directly (not imported as a module).
It passes the command-line arguments (excluding the script name itself) to the main() function.

Usage:
python3 pass-checker password123