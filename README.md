# Highly Experimental!

This is my attempt at a Cookiecutter data science project - see <https://github.com/drivendata/cookiecutter-data-science>

This uses Git submodules, specifically to pull in the `data-science-pet-containers` Docker repository. So do `git clone --recursive-submodules` with it.

What's here besides the oodles of Cookiecutter scaffolding and the submodules? Well, so far I've figured out how to sync the raw data to AWS S3, run a PostGIS job to load the TriMet ridership data into a database and make a backup file of it, and sync the resulting backup back to AWS S3. See <https://github.com/hackoregon/transportation-data-science-environment/blob/master/src/data/ridership/README.md>.
