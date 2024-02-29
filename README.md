# data
# Define the Flume agent
agent.sources = source1
agent.channels = channel1
agent.sinks = sink1

# Configure the source to read from a file
agent.sources.source1.type = exec
agent.sources.source1.command = tail -F example.log
agent.sources.source1.channels = channel1

# Configure the channel
agent.channels.channel1.type = memory

# Configure the sink for HDFS
agent.sinks.sink1.type = hdfs
agent.sinks.sink1.hdfs.path = /your/hdfs/path
agent.sinks.sink1.hdfs.fileType = DataStream
agent.sinks.sink1.hdfs.writeFormat = Text
agent.sinks.sink1.hdfs.filePrefix = events
agent.sinks.sink1.hdfs.rollInterval = 600
agent.sinks.sink1.hdfs.rollSize = 134217728
agent.sinks.sink1.hdfs.rollCount = 0

# Bind the source and sink to the channel
agent.sources.source1.channels = channel1
agent.sinks.sink1.channel = channel1

bin/flume-ng agent --conf conf --conf-file flume.conf --name agent_name -Dflume.root.logger=INFO,console
