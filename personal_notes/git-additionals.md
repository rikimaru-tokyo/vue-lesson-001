…or create a new repository on the command line

echo "# vue-lesson-001" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:rikimaru-tokyo/vue-lesson-001.git
git push -u origin main


…or push an existing repository from the command line
git remote add origin git@github.com:rikimaru-tokyo/vue-lesson-001.git
git branch -M main
git push -u origin main