from flask import Flask, render_template
import subprocess
import os
import pytz
from datetime import datetime

app = Flask(_name_)

@app.route('/htop')
def htop():
    process = subprocess.Popen(['htop'], stdout=subprocess.PIPE, stderr=subprocess.PIPE)
    stdout, stderr = process.communicate()
    htop_output = stdout.decode('utf-8')

    name = "Your Full Name"  # Replace with your actual name
    username = os.getlogin()
    ist = pytz.timezone('Asia/Kolkata')
    server_time = datetime.now(ist).strftime("%Y-%m-%d %H:%M:%S %Z%z")

    return render_template('htop.html', name=name, username=username, server_time=server_time, htop_output=htop_output.splitlines())

if _name_ == '_main_':
    app.run(debug=True, host='0.0.0.0', port=5000)
