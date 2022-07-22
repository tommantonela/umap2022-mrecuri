# Repository for the UMAP 2022 paper: *Haven’t I just listened to this?: Exploring diversity in music recommendations*

Recommender systems have recently been criticized for promoting bias and trapping users into filter bubbles. This phenomenon not only limits potential user interactions but also threatens the broadness of content consumption. In a music recommender, for example, this situation can limit user perspective as music allows people to develop cultural knowledge and empathy. As a fundamental characteristic of users’ content consumption is its diversity, it is necessary to break the bubbles and recommend potentially relevant and diverse songs from outside the influence of such bubbles. To address this problem, we present MRecuri (Music RECommender for filter bUbble diveRsIfication), a music recommendation technique to foster the diversity and novelty of recommendations. A preliminary evaluation over Last.fm listening data showed the potential of MRecuri to increase the diversity and novelty of recommendations compared with state-of-the-art techniques.


## Architecture

``MRecuri``’s overall architecture is schematized in the following Figure. It takes as input the track knowledge graph, user listening history and interactions. For each user, it outputs a ranking of tracks according to their listening likelihood strength

![Architecture](https://github.com/tommantonela/umap2022-mrecuri/blob/main/main/architecture.png)

## Data

Evaluation was based on data collected from Last.fm. We focused on the track listening history and the users’ social networks. Based on the social interactions collected by [Zhan et al.](https://dl.acm.org/doi/10.1145/2783258.2783268), we selected the top 5% of users with the highest number of social connections and scrobbles. We collected the scrobble history for each of the 3, 307 selected users using the Last.fm API. From the set of over 1 million tracks listened by the selected users, we selected approximately 252𝑘 tracks with the highest number of listeners among the selected users, with 99% of users associated with over 40 songs. For each selected track, we collected the total number of scrobbles and listeners, tags, artist (and their tags) and Spotify audio features. 

### Data format

The following data can be found in the file ``dataset.pickle`` inside ``data/dataset.rar``.

* ``dataset['full']``, ``dataset['train']``, ``dataset['test']`` are graphs:
    * Nodes: 'type' indicates whether the node represents a 'user' or a 'track'
    * Edges: graphs are not directed and edges always connect a ``user`` and a ``track``. Note that it is not guaranteed that the source is always a ``user``.
      * ``date`` represents the date of the last time the user listened to the track.
      * ``pos`` is redundant with ``date``, represents the order in which the user listened to the track.
      * ``scrobbles`` represents the number of times that the ``user`` listened to the ``track``.

* ``dataset['users']`` is a ``dict`` mapping the graph ids to usernames: ``{username : user id in the graph}``
   
* ``dataset['artist-tracks']`` is dict '{artist : {track : track id in the graph}}'

Note. The original set of users and social interactions can be retrieved from: the [Cosnet](https://www.aminer.cn/cosnet) site.

## Model
In the ``model`` folder, you can find the final model reported in the paper.

## Notebooks

The notebooks allow to replicate the evaluation of the proposed model.

* ``01-Data-Full-Train.ipynb``. Divides data intro train and test sets.
* ``02-Embeddings.ipynb``.  Computes user-track embeddings that are used to determine whether they are close to each other in the graph.
* ``03-Train-dataset-GraphDropout-Complex-Beta075.ipynb``. Trains the model.
* ``04-Predict-GraphDropout-Complex-Beta075.ipynb``. Makes predictions.


If using our code or model, please cite our publication:
```
@inproceedings{10.1145/3511047.3536409,
  author = {Tommasel, Antonela and Rodriguez, Juan Manuel and Godoy, Daniela},
  title = {Haven’t I just listened to this?: Exploring diversity in music recommendations},
  year = {2022},
  isbn = {},
  publisher = {Association for Computing Machinery},
  address = {New York, NY, USA},
  url = {https://doi.org/10.1145/3511047.3536409},
  doi = {10.1145/3511047.3536409},
  pages = {},
  numpages = {},
  keywords = {recommender ssytems, filter bubbles, music recommendation, diversity},
  location = {Barcelona, Spain},
  series = {UMAP '22}
}
```

## Contact info:

* [Antonela Tommasel](https://tommantonela.github.io) (antonela.tommasel@isistan.unicen.edu.ar)
* [Juan Manuel Rodriguez](https://sites.google.com/site/rodriguezjuanmanuel/home) (juanmanuel.rodriguez@isistan.unicen.edu.ar)

The repository is licenced under the Apache License V2.0. 
