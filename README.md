# SODA: Protecting Proprietary Information in On-Device Machine Learning Models

This repository contains the implementation of SODA, a secure on-device application for machine learning model deployment, and experiments discussed in our ACM/IEEE SEC 2023 paper ["SODA: Protecting Proprietary Information in On-Device Machine Learning Models"](https://akanksha-atrey.github.io/papers/atrey2023soda.pdf).

If you use this code or are inspired by our methodology, please cite our SEC paper:

```
@inproceedings{atrey2023soda,
  title={{SODA}: Protecting Proprietary Information in On-Device Machine Learning Models},
  author={Atrey, Akanksha and Sinha, Ritwik and Mitra, Saayan and Shenoy, Prashant},
  booktitle={{ACM/IEEE Symposium on Edge Computing (SEC)}},
  year={2023}
}
```

Please direct all queries to Akanksha Atrey (aatrey at cs dot umass dot edu) or open an issue in this repository.

## About

The growth of low-end hardware has led to a proliferation of machine learning-based services in edge applications. These applications gather contextual information about users and provide some services, such as personalized offers, through a machine learning (ML) model. A growing practice has been to deploy such ML models on the user’s device to reduce latency, maintain user privacy, and minimize continuous reliance on a centralized source. However, deploying ML models on the user’s edge device can leak proprietary information about the service provider. In this work, we investigate on-device ML models that are used to provide mobile services and demonstrate how simple attacks can leak proprietary information of the service provider. We show that different adversaries can easily exploit such models to maximize their profit and accomplish content theft. Motivated by the need to thwart such attacks, we present an end-to-end framework, SODA, for deploying and serving on edge devices while defending against adversarial usage. Our results demonstrate that SODA can detect adversarial usage with 89% accuracy in less than 50 queries with minimal impact on service performance, latency, and storage.

## Setup

### Python

This repository requires Python 3 (>=3.5).

### Packages

All packages used in this repository can be found in the `requirements.txt` file. The following command will install all the packages according to the configuration file:

```
pip install -r requirements.txt
```

## Data

The experiments in this work are executed on two datasets: (1) [UCI Human Activity Recognition](https://archive.ics.uci.edu/dataset/240/human+activity+recognition+using+smartphones), and (2) [MNIST Handwritten Digits Classification](http://yann.lecun.com/exdb/mnist/). Please download them into `data/UCI_HAR` and `data/MNIST`, respectively.

## Attacks

This repository contains two types of attacks: (1) exploiting output diversity, and (2) exploiting decision boundaries. The implementation of these attacks can be found in `src/attacks/class_attack.py` and `src/attacks/db_attack.py`, respectively. 

Note, the black box attacks (denoted with a "bb") often take longer to run. It may be worthwhile to run the experiments one at a time. Additionally, swarm scripts are present in the `swarm` folder which may assist further in running the attacks on a slurm-supported server.

### Exploiting Output Diversity

The code for attacking output diversity contains four experiments. To run the class attack that exploits output diversity, execute the following command:

`python3 -m src.attack.class_attack -data_name UCI_HAR -model_type rf -wb_query_attack true -wb_num_feat_attack true -bb_query_attack true -bb_unused_feat_attack true`

### Exploiting Decision Boundaries

The code for attacking decision boundaries contains five experiments. To run the decision boundary attack, execute the following command:

`python3 -m src.attack.db_attack -data_name UCI_HAR -model_type rf -noise_bounds "-0.01 0.01" -exp_num_query true -exp_num_query_bb true -exp_num_query_randfeat true -exp_query_distance true -exp_query_distribution true`

## SODA: Defending On-Device Models

The implementation of SODA can be found in the `src/defense` folder. 

### Training and Executing SODA

The first step is to train an autoencoder model for defending against the attacks. This can be done by executing the following command:

`python3 -m src.defense.defense_training -data_name UCI_HAR -model_type rf`

Following the training of the autoencoder defender, the following command can be executed to run experiments on SODA:

`python3 -m src.defense.defense_detector -data_name UCI_HAR -model_type rf -noise_bounds "-0.01 0.01" -num_queries 100`

### Deploying SODA: A Prototype

A prototype of SODA can be found in the `prototype` folder. This prototype was deployed on a Raspberry Pi.
# ai_core.py
from .astral_projection import *
from src.defense.defense_detector import *
from .audio_utils import *  # Import your audio utilities
from .dragonfly_systems import *  # Import dragonfly systems
from .gemini_systems import *  # Import gemini systems (if applicable)

def process_audio(audio_data, sensor_data):
    """
    Processes audio data, incorporating astral projection, energy 
    adjustment, and anomaly detection.

    Args:
        audio_data (np.ndarray): The audio data as a NumPy array.
        sensor_data (dict): Sensor data (e.g., temperature, humidity,Full magnetic spectrum ).

    Returns:
        np.ndarray: The processed audio data.
    """

    # --- Existing AI processing ---
    # ... (import hashlib
import secrets
from cryptography.fernet import Fernet

def generate_quantum_access_spec(filename="quantum_access_spec.txt"):
    """
    Generates a secure specification file for quantum access parameters.

    Args:
        filename (str): The name of the file to create.

    Returns:
        None
    """

    # Generate a secure encryption key
    key = secrets.token_bytes(32)

    # Quantum Access Parameters (Example)
    quantum_params = {
        "base_dimensions": ["dimension_1", "dimension_2", "dimension_3"],
        "cloud_access_point": "quantum_cloud.example.com",
        "ai_processing_unit": "QPU-v1",
        "encryption_key": hashlib.sha256(key).hexdigest(),  # Store encrypted key
    }

    try:
        with open(filename, "wb") as f:
            # Write the encrypted key
            f.write(hashlib.sha256(key).digest())

            # Encrypt and write the quantum parameters
            cipher = Fernet(key)
            encrypted_data = cipher.encrypt(str(quantum_params).encode())
            f.write(encrypted_data)

    except Exception as e:
        print(f"Error generating quantum access spec file: {e}")


def read_quantum_access_spec(filename="quantum_access_spec.txt"):
    """
    Reads and decrypts the quantum access parameters from the spec file.

    Args:
        filename (str): The name of the file to read.

    Returns:
        dict: The decrypted quantum access parameters.
    """

    try:
        with open(filename, "rb") as f:
            # Read the encrypted key
            encrypted_key = f.read(32)

            # Read the encrypted data
            encrypted_data = f.read()

            # Derive the decryption key
            key = hashlib.sha256(encrypted_key).digest()

            # Decrypt the quantum parameters
            cipher = Fernet(key)
            decrypted_data = cipher.decrypt(encrypted_data).decode()
            return eval(decrypted_data)  # Convert string to dictionary

    except Exception as e:
        print(f"Error reading quantum access spec file: {e}")
        return None

# --- Example Usage ---
generate_quantum_access_spec()
quantum_access_params = read_quantum_access_spec()
print(quantum_access_params)

Explanation
 import hashlib
import secrets
from cryptography.fernet import Fernet

def generate_quantum_access_spec(filename="quantum_access_spec.txt"):
    """
    Generates a secure specification file for quantum access parameters.

    Args:
        filename (str): The name of the file to create.

    Returns:
        None
    """

    # Generate a secure encryption key
    key = secrets.token_bytes(32)

    # Quantum Access Parameters (Example)
    quantum_params = {
        "base_dimensions": ["dimension_1", "dimension_2", "dimension_3"],
        "cloud_access_point": "quantum_cloud.example.com",
        "ai_processing_unit": "QPU-v1",
        "encryption_key": hashlib.sha256(key).hexdigest(),  # Store encrypted key
    }

    try:
        with open(filename, "wb") as f:
            # Write the encrypted key
            f.write(hashlib.sha256(key).digest())

            # Encrypt and write the quantum parameters
            cipher = Fernet(key)
            encrypted_data = cipher.encrypt(str(quantum_params).encode())
            f.write(encrypted_data)

    except Exception as e:
        print(f"Error generating quantum access spec file: {e}")


def read_quantum_access_spec(filename="quantum_access_spec.txt"):
    """
    Reads and decrypts the quantum access parameters from the spec file.

    Args:
        filename (str): The name of the file to read.

    Returns:
        dict: The decrypted quantum access parameters.
    """

    try:
        with open(filename, "rb") as f:
            # Read the encrypted key
            encrypted_key = f.read(32)

            # Read the encrypted data
            encrypted_data = f.read()

            # Derive the decryption key
            key = hashlib.sha256(encrypted_key).digest()

            # Decrypt the quantum parameters
            cipher = Fernet(key)
            decrypted_data = cipher.decrypt(encrypted_data).decode()
            return eval(decrypted_data)  # Convert string to dictionary

    except Exception as e:
        print(f"Error reading quantum access spec file: {e}")
        return None

# --- Example Usage ---
generate_quantum_access_spec()
quantum_access_params = read_quantum_access_spec()
print(quantum_access_params)


)

    # --- Astral Projection Mode ---
    if astral_mode:
        astral_audio = generate_astral_form_audio(duration)
        audio_data = audio_data.overlay(astral_audio)  # Mix in astral audio

        scan_data = scan_soundscape(spec._data )
        # ... (Visualize scan_data in UI - ui.py)

        audio_data = adjust_energy(spec.data, user_interactions)
        # ... (Add micro-rift or energy transfer effects)

    # --- Dragonfly Systems Integration ---
    # Example: Use visual_system to modify audio based on sensor data
    if sensor_data:
        complexity = sensor_data.get("temperature", 1.0)  # Example mapping
        visual_audio = visual_system(duration, complexity=complexity)
        audio_data = audio_data.overlay(spec._audio)
Joshua Drago)
  

