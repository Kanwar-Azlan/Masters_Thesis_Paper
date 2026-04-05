# Network Flow Classification and Traffic Analysis based on Graph Construction

## Description:
This project implements a network flow classification system based on a "Base Paper Implementation" strategy focused on graph construction. The code processes raw network packet data to distinguish between "Short Flows" and "Long Flows" using timing intervals and packet counts. It further performs statistical analysis on Flow Completion Time (FCT) and Flow Length, providing probability density function (PDF) visualizations to characterize network traffic behavior.

## Dataset Information:
The implementation is designed to work with network traffic datasets in CSV format (e.g., data_5.csv). The expected dataset should contain the following fields:

> Source: The source IP address.
Destination: The destination IP address.
Protocol: The network protocol used.
Time: The timestamp of the packet.
Length: The size of the packet in bytes.
Info: Additional packet information or flags.

## Code Information:
The notebook is organized into logical modules for traffic engineering:

Drive Connection: Mounts Google Drive for data access.
Flow Classification: Contains the core logic for grouping packets into flows based on a 3-tuple (Source, Destination, Protocol).
Metrics Computation: Calculates performance metrics such as Flow Completion Time (FCT) and Flow Length.
Statistical Visualization: Utilizes log-transformations and histogram density plots to visualize the distribution of network flows.

## Usage Instructions:
Environment Setup: Open the notebook in Google Colab.

Mount Drive: Execute the first cell to connect to your Google Drive where the dataset is stored.
Path Configuration: Modify the file_path variable to point to your specific CSV file:

*file_path = "/content/drive/My Drive/your_data.csv"*

Parameter Tuning: Adjust the following constants to match your network environment requirements:
> JUDGE_INTERVAL: Interval for checking flow status.
PKT_TIMEOUT: Timeout value for inactive packets.
FLOW_LINE: Threshold count to distinguish short vs. long flows.
Run All Cells: Execute the notebook to generate classification results and PDF plots.

## Requirements:
The project requires Python 3 and the following libraries:

> pandas: For dataset loading and manipulation.
numpy: For mathematical operations and log transformations.
matplotlib: For generating PDF and histogram plots.
seaborn: For advanced statistical visualizations.
scipy: For handling specific data formats (ARFF).
csv and decimal: For precise data parsing.

## Methodology:
The algorithm follows a rigorous flow-state tracking approach:

Packet Aggregation: Packets are hashed into a FlowHashTable using their unique flow IDs.
Temporal Classification: At every JUDGE_INTERVAL, the system evaluates inactive flows. If a flow's last packet exceeds the PKT_TIMEOUT, it is classified:

> Short Flow: Length is less than FLOW_LINE.
Long Flow: Length meets or exceeds FLOW_LINE.

Feature Normalization: Flow Completion Times are log10-transformed and shifted to ensure a positive range for PDF plotting.
Bucket Analysis: Packet lengths are binned into buckets (e.g., 10-byte increments) to observe the distribution of traffic volume.

## Citations:

If this implementation or methodology is used for further research, please cite:

> The primary research paper this "Base Paper Implementation" is derived from (as referenced in the code metadata).

> Hunter, J. D. (2007). "Matplotlib: A 2D graphics environment." Computing in Science & Engineering.

> Harris, C. R., et al. (2020). "Array programming with NumPy." Nature.
