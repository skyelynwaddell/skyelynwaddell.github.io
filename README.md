# Skyesblog
#### Developed with Hugo, HTML, and JS

## Starting the server
simply run
```
hugo server
```
in some instances if things dont work try it in dev mode
```
hugo -D server
```

## Creating a new post
To create a new post run the following command
```
hugo new post-name.md
```
This will generate an MD file with the correct headers, and the current date/time.
Navigate to 
```
/content/post-name.md
```
Then you can modify your new blog post!

## Updating blog after making a new post
When you update or make changes to the website, you must run the following command to save these changes to the public version
```
hugo
```

## Uploading newest copy of blog
Simply add, commit, and push all files in the root of the blog.
```
git add .
git commit -m "my newest blog post"
git push
```