## Deployment Best Practices

### Rules to Live By
1. Always use git
2. There are 3 environments. Development, Staging, and Production
3. Have fun and stay on your toes

### Development
This is your local environment on your computer. You should have at least 3 branches locally. Master, staging and what ever feature or bug fix you are working on. To get started clone down the project from github. Make sure to clone both the staging and master branches. Next, branch off the staging branch to start working. Keep the name descriptive and concise. Usually a 2-3 word feature description will suffice. For example *blog-comments*. Once you're finished and the feature is stable, merge into the staging evironment, and push to the staging server for quality assurance testing. The easiest way to do this is:
```
git merge blog-comments
git push staging_branch staging:master
```

### Staging
This is where testing takes place and in a production-simulated environment; even using the production database from time to time. Code should be pushed here after every feature completion or bug fixes. The more iterative the better. Once determined by the testers to be absoulutely stable, the code should be push to the production environment.
```
git merge staging
git push production master
```

### Production
This is the home of the live application. Be sure to be absolutely sure that your branch is stable before pushing this live. In rare cases, such as emergency bug fixes you can push changes straight to productions. However, the best way to get a make sure your changes are completely stable is to test first on the staging server.

### Github
Github is really your best friend during this entire process. It allows you to collaborate effectively with your teammates. It hosts all your git branches. You should be pushing to github at the very least once a day. Also push to github either before or after pushing to staging and production environments. Finally, don't forget to pull down from staging and masters ever so often. Usually you're not the only one working on a project.
```
git push origin staging
```

### Bitbucket
Bitbucket is where projects go to sleep. Once a project is wrapped up, we don't want it clogging up the repo list on github. We don't want to just delete it either. We're always going back to reference old code or help out clients when needed. Bitbucket provides us an archive where we can store these projects. See Eric Candino when your project is ready to be transfered. 