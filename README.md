# spaCy_for_medical_ner

Main steps of the code:

-Extracting entities "Medicine,MedicalCondition,Pathogen" and their corresponding start and end positions within the example's content.
-Adding the extracted entities to sets "medicine,medicalCondition,pathogen" and then building the train_data 
consisting of the example's "content" and the extracted entities.

-In RulerModel class we define a named entity recognition model. 
Generate_patterns: generates a list of patterns to be used by the entity ruler.
Add_patterns_into_ruler: Adds the generated patterns to the entity ruler.

-Generate_dataset class takes in a ruler_model as input and generates a dataset for training a named entity recognition model.
Find_entity_types: Uses ruler_model to return the entities present in the input text, along with their start and end positions and labels.
Assign_labels_to_documents: Takes in a dataset of texts, applies the find_entity_types on each text, assigns the entities found to the corresponding text.

-NERModel class generates and trains a named entity recognition model using spaCy. It takes in an optional input of number of iterations to train the model.
__init__ : Initializes the model, sets the number of iterations, generates an empty spaCy model, adds a NER and a transformer pipeline.
add_pipe: Adds a new pipeline to the model, and appends the name of the pipeline to the pipe_name list.
remove_pipe: Removes a pipeline from the model, and remove the name of the pipeline from the pipe_names list.
fit: Takes in train data and uses it to train the model. It starts by adding the entities present in the train data to the NER pipeline.
It then disables all other pipelines, initializes the transformer pipeline with the train examples, and sets the optimizer. 
-accuracy_score: Takes in a validation data and uses it to calculate the accuracy of the model.It uses a Scorer object to calculate the accuracy.

-Extend_model function first assigns the ruler_model to the ner_model of the train object. 
It then builds a new my_entity_ruler component for the spaCy language pipeline using ruler_component function which applies the entity_ruler from 
the ruler_model to the input doc. It then adds the items from the passed in entity_type sets to the vocabulary of the train object's model.

This function is used to add additional entities to the exisitng model, by setting a new pipeline and adding it to the model before the NER pipeline.
With this the model can recognize additional entities from the passed in sets and improve its performance on the extended dataset.
