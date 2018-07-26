## Nbgrader
Nbgrader is a tool that allows creating, distributing and grading assignments in the Jupyter notebook.

### Installation
To install updated version of nbgrader("Collect All" added):

```!pip install --user  git+git://github.com/cybera/nbgrader.git@cybera-changes
```

### How to use it
Documentation and introductory video:

http://nbgrader.readthedocs.io/en/stable/

### Additional feature - Collect All

![](images/collect_all.png)

If the student had submitted an assignment multiple times - all the submitted assignments are stored on the shared location.
When the teacher collects assignments - only the latest submission is copied to the teachers home directory and graded.
"Collect All"  allows to copy all the assignments submitted in the past to the teachers home directory.
The assignments are copied to ~/<Course_name>/submitted_history/<assignment>/<studentID_timestamp> directory on the teachers container.
