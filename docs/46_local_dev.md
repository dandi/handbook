If you'd like to develop these docs, the follow commands should get you started locally -- with hot-reloading too :)

You'll need to create and configure a Python environment according to configuration provided in `requirements.txt` file in the root of this directoy, e.g. via

    python3 -m venv venv && source venv/bin/activate && python3 -m pip install -r requirements.txt

And your current session would already be using that virtual Python environment, which you could deactivate by executing `deactivate` command.
If in the future you would need to activate it, just `source venv/bin/activate` again.

After that you can either
- do one time manual build using `mkdocs build` and find built website under `site/` folder.
- run `mkdocs serve` which would not only build website and start a local webserver for you to visit rendered version at e.g., http://127.0.0.1:8000/

