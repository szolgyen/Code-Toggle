# Hide code cells of Notebooks

<b>Scope</b>: Exported Jupyter Notebooks in HTML format <br>
<b>Function</b>: Hide/show input code cells 

This JavaScript code snippet adds an active button to an HTML document which is exported from a Jupyter Notebook. It allows for hiding and showing the content of all code cells of the whole notebook.

Copy this code to a markdown cell in the top of your Jupyter Notebook. 

```
<script>
    function toggle_all() {
        var codeCells = document.querySelectorAll('.jp-InputArea-editor');
        var firstCell = codeCells[0].parentNode;
        var anyCellVisible = firstCell.style.visibility === 'visible';

        for (var i = 0; i < codeCells.length; i++) {
            var cell = codeCells[i].parentNode;
            if (anyCellVisible) {
                cell.style.visibility = 'hidden';
                cell.style.position = 'absolute';
            } else {
                cell.style.visibility = 'visible';
                cell.style.position = '';
            }
        }

        var button = document.getElementById('toggleButton');
        button.innerHTML = anyCellVisible ? 'Show Code' : 'Hide Code';
    }

    function refresh() {
        var button = document.createElement('button');
        button.innerHTML = 'Show Code';
        button.id = 'toggleButton';
        button.onclick = function() {
            toggle_all();
            return false;
        };

        // Insert the button at the beginning of the notebook
        var notebook = document.querySelector('.jp-Notebook');
        notebook.insertBefore(button, notebook.firstChild);

        // Initially hide all code cells
        toggle_all();
    }

    // Call refresh when the document is loaded
    document.addEventListener("DOMContentLoaded", function() {
        refresh();
    });
</script>

```




