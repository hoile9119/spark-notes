<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Spark Submit Command Generator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        .form-group {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }
        label {
            flex: 1;
            /* Adjusts label width */
            margin-right: 10px;
            /* Space between label and input */
        }
        select, input {
            flex: 0.4;
            /* Adjusts input width for text and select */
            padding: 2.5px;
            box-sizing: border-box;
            border: none;
            /* Ensures padding is included in the width */
        }
        button {
            padding: 10px 15px;
        }
        #output {
            width: 100%;
            /* Make the output box full width */
            height: 150px;
            /* Set a height for the output box */
            padding: 10px;
            /* Add padding for better readability */
            border: 1px solid #ccc;
            /* Add a border */
            overflow: auto;
            /* Allow scrolling if content overflows */
            white-space: pre-wrap;
            /* Preserve whitespace and wrap text */
            background-color: #f9f9f9;
            /* Light background for better visibility */
        }
        .spark-defaults-conf,
        .additional-conf,
        .basic-conf {
            background-color: #f0f8ff;
            /* Light blue background for both sections */
            padding: 10px;
            /* Padding around the sections */
            border: 1px solid #ccc;
            /* Border for visual separation */
            margin-top: 10px;
            /* Space above the sections */
        }
        .generator {
            margin-top: 20px;
            /* Add space above the button */
            margin-bottom: 20px;
            /* Add space below the button */
            text-align: center;
            /* Center the button */
        }
    </style>
</head>

<body>
    <h1>SPARK CONF GENERATOR</h1>
    <form id="sparkSubmitForm">
        <div class="basic-conf">
            <h4>BASIC CONFIG</h4>
            <div class="form-group">
                <label for="appName">Application Name:</label>
                <input type="text" id="appName" value="mySparkApplication" required>
            </div>
            <div class="form-group">
                <label for="master">Master URL:</label>
                <select id="master" required>
                    <option value="yarn">YARN</option>
                    <option value="local">local</option>
                    <option value="mesos">Mesos</option>
                    <option value="k8s">Kubernetes</option>
                </select>
            </div>
            <div class="form-group">
                <label for="deployMode">Deploy Mode:</label>
                <select id="deployMode" required>
                    <option value="cluster">cluster</option>
                    <option value="client">client</option>
                </select>
            </div>
        </div>
        <div class="spark-defaults-conf">
            <h4>SPARK-DEFAULTS.CONF</h4>
            <div class="form-group">
                <label for="driverCores">spark.driver.cores:</label>
                <input type="number" id="driverCores" value="1">
            </div>
            <div class="form-group">
                <label for="driverMemory">spark.driver.memory (GB):</label>
                <input type="number" id="driverMemory" value="4">
            </div>
            <div class="form-group">
                <label for="driverMaxResultSize">spark.driver.maxResultSize (GB):</label>
                <input type="number" id="driverMaxResultSize" value="4">
            </div>
            <div class="form-group">
                <label for="driverMemoryOverhead">spark.driver.memoryOverhead (MB):</label>
                <input type="number" id="driverMemoryOverhead" value="921">
            </div>
            <div class="form-group">
                <label for="executorInstances">spark.executor.instances:</label>
                <input type="number" id="executorInstances" value="2">
            </div>
            <div class="form-group">
                <label for="executorMemory">spark.executor.memory (GB):</label>
                <input type="number" id="executorMemory" value="4">
            </div>
            <div class="form-group">
                <label for="executorCores">spark.executor.cores:</label>
                <input type="number" id="executorCores" value="4">
            </div>       
            <div class="form-group">
                <label for="executorMemoryOverhead">spark.executor.memoryOverhead (MB):</label>
                <input type="number" id="executorMemoryOverhead" value="921">
            </div>
            <div class="form-group">
                <label for="dynamicAllocation">spark.dynamicAllocation.enabled:</label>
                <input type="text" id="dynamicAllocation" value="false">
            </div>            
            <div class="form-group">
                <label for="adaptiveQueryExecution">spark.sql.adaptive.enabled:</label>
                <input type="text" id="adaptiveQueryExecution" value="true">
            </div>
        </div>
        <div class="additional-conf">
            <h4>ADDITIONAL CONFIGURATION</h4>
            <div class="form-group">
                <label for="portMaxRetries">spark.port.maxRetries:</label>
                <input type="number" id="portMaxRetries" value="100">
            </div>
            <div class="form-group">
                <label for="hiveDynamicPartition">spark.hadoop.hive.exec.dynamic.partition:</label>
                <input type="text" id="hiveDynamicPartition" value="true">
            </div>
            <div class="form-group">
                <label for="hiveDynamicPartitionMode">spark.hadoop.hive.exec.dynamic.partition.mode:</label>
                <input type="text" id="hiveDynamicPartitionMode" value="nonstrict">
            </div>
            <div class="form-group">
                <label for="sparkJar">spark.jars:</label>
                <input type="text" id="sparkJar" value="/path/to/your/jar1.jar,/path/to/your/jar2.jar">
            </div>
        </div>
        <div class="generator">
            <button type="submit" id="generateSubmit">Generate Spark Submit</button>
            <button type="submit" id="generateConf">Generate Spark Config</button>
        </div>
    </form>
    <h3>Result:</h3>
    <pre id="output"></pre>
    <script>
        document.getElementById('generateSubmit').addEventListener('click', function (event) {
            event.preventDefault();
            const appName = document.getElementById('appName').value;
            const master = document.getElementById('master').value;
            const deployMode = document.getElementById('deployMode').value;
            const driverCores = document.getElementById('driverCores').value;
            const driverMemory = document.getElementById('driverMemory').value;
            const driverMemoryOverhead = document.getElementById('driverMemoryOverhead').value;
            const driverMaxResultSize = document.getElementById('driverMaxResultSize').value;
            const executorInstances = document.getElementById('executorInstances').value;
            const executorMemory = document.getElementById('executorMemory').value;
            const executorCores = document.getElementById('executorCores').value;
            const executorMemoryOverhead = document.getElementById('executorMemoryOverhead').value;
            const dynamicAllocation = document.getElementById('dynamicAllocation').value;
            const adaptiveQueryExecution = document.getElementById('adaptiveQueryExecution').value;
            const portMaxRetries = document.getElementById('portMaxRetries').value;
            const hiveDynamicPartition = document.getElementById('hiveDynamicPartition').value;
            const hiveDynamicPartitionMode = document.getElementById('hiveDynamicPartitionMode').value;
            const sparkJar = document.getElementById('sparkJar').value;
            const command = `spark3-submit \\\n` +
            `--name "${appName}" \\\n` +
            `--master ${master} \\\n` +
            `--deploy-mode ${deployMode} \\\n` +
            `--driver-cores ${driverCores} \\\n` +
            `--driver-memory ${driverMemory}g \\\n` +
            `--num-executors ${executorInstances} \\\n` +
            `--executor-memory ${executorMemory}g \\\n` +
            `--executor-cores ${executorCores} \\\n` +
            `--conf spark.driver.memoryOverhead=${driverMemoryOverhead}m \\\n` +
            `--conf spark.executor.memoryOverhead=${executorMemoryOverhead}m \\\n` +
            `--conf spark.driver.driverMaxResultSize=${driverMaxResultSize}g \\\n` +
            `--conf spark.dynamicAllocation.enabled=${dynamicAllocation} \\\n` +
            `--conf spark.sql.adaptive.enabled=${adaptiveQueryExecution} \\\n` +
            `--conf spark.port.maxRetries=${portMaxRetries} \\\n` +
            `--conf spark.hadoop.hive.exec.dynamic.partition=${hiveDynamicPartition} \\\n` +
            `--conf spark.hadoop.hive.exec.dynamic.partition.mode=${hiveDynamicPartitionMode} \\\n` +
            `--jars ${sparkJar} \\\n` +
            `main.py`;
            document.getElementById('output').textContent = command;
        });
        document.getElementById('generateConf').addEventListener('click', function (event) {
            event.preventDefault();
            const appName = document.getElementById('appName').value;
            const master = document.getElementById('master').value;
            const deployMode = document.getElementById('deployMode').value;
            const driverCores = document.getElementById('driverCores').value;
            const driverMemory = document.getElementById('driverMemory').value;
            const driverMemoryOverhead = document.getElementById('driverMemoryOverhead').value;
            const driverMaxResultSize = document.getElementById('driverMaxResultSize').value;
            const executorInstances = document.getElementById('executorInstances').value;
            const executorMemory = document.getElementById('executorMemory').value;
            const executorCores = document.getElementById('executorCores').value;
            const executorMemoryOverhead = document.getElementById('executorMemoryOverhead').value;
            const dynamicAllocation = document.getElementById('dynamicAllocation').value;
            const adaptiveQueryExecution = document.getElementById('adaptiveQueryExecution').value;
            const portMaxRetries = document.getElementById('portMaxRetries').value;
            const hiveDynamicPartition = document.getElementById('hiveDynamicPartition').value;
            const hiveDynamicPartitionMode = document.getElementById('hiveDynamicPartitionMode').value;
            const sparkJar = document.getElementById('sparkJar').value;
            const confDict = 
        `{
            "spark.master": "${master}",
            "spark.driver.cores": ${driverCores},
            "spark.driver.memory": "${driverMemory}g",
            "spark.executor.instances": ${executorInstances},
            "spark.executor.cores": ${executorCores},
            "spark.executor.memory": "${executorMemory}g",
            "spark.port.maxRetries": ${document.getElementById('portMaxRetries').value},            
            "spark.hadoop.hive.exec.dynamic.partition": ${hiveDynamicPartition === "true" ? "True" : "False"},
            "spark.hadoop.hive.exec.dynamic.partition.mode": "${hiveDynamicPartitionMode}",
            "spark.dynamicAllocation.enabled": ${dynamicAllocation === "true" ? "True" : "False"}
        }`;
            document.getElementById('output').textContent = confDict;
        });
    </script>
</body>

</html>