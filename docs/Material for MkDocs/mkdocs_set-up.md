# The Workflow for updating this site 

## Updating and building MkDocs then pushing to GitHub 

Make sure that the virtual environment has been activated with: 

```bash
source venv/bin/activate  
```

Update the markdown files and then run the following command in order the run a live server to preview changes. 

```bash
mkdocs serve 
```

This will automatically rebuild the site when changes are made. To manually build the site use: 

```bash
mkdocs build  
```

Then to push the changes to go live via GitHub Pages we use: 

```bash
git add . 
git commit -m "message" 
git push orgin main 
```

This can take a minute or two to update on the live website. 
