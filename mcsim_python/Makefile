
.PHONY: environment remove-env install uninstall test # .PHONY is something we can add when our target dependencies are not files.

MODULE=mcsim
ENVIRONMENT=chem274A_lab1

## environment target: removes previous environment and uses conda to create a new environment with python package dependencies
environment: remove-env
	conda create -n $(ENVIRONMENT) "python=3.9" --yes
	conda install -c conda-forge notebook nbconvert numpy matplotlib pytest-cov pandas --name $(ENVIRONMENT) --yes

## remove the current environment. This is called from the environment make target
remove-env:
	conda remove --name $(ENVIRONMENT) --all --yes

##uses pip to install the python directory as a package
install: uninstall ## install the package to the active Python's site-packages
	pip install .

## uses pip to install a developer package, which enables edits
dev-install: uninstall
	pip install -e .

##uses pip to uninstall the package, this is a dependency for make targets install and dev-install
uninstall: ## uninstall the package
	pip uninstall --yes $(MODULE)

## calls pytest to run automated tests in the tests folder: test_psl.py and test_run.py
test: 
	pytest -v
