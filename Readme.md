# SnakeTrainer: Ein Snake-Spiel mit einfacher KI

## Projektziel

Du erhältst ein vorbereitetes Snake-Spiel.

Deine Aufgabe ist nicht, alles von null zu programmieren.

Du sollst:

* das Projekt korrekt erstellen
* das Spiel starten
* Tests ausführen
* kleine Funktionen verstehen
* sichtbare Änderungen machen
* Trainingsdaten verwenden
* ein KI-Modell trainieren
* den KI-Modus testen
* deine Arbeit kurz dokumentieren

Am Schluss sollst du sagen können:

> Das ist mein Spiel. Ich habe es angepasst. Ich weiss grob, wie die KI verwendet wird.

# 1. Was du verstehen sollst

Du musst nicht alles im Code verstehen.

Das ist wichtig.

## Das sollst du verstehen

```text
Ein Spielzustand wird in Zahlen umgewandelt.
Viele Beispiele werden gespeichert.
Ein Modell wird mit diesen Beispielen trainiert.
Das Modell macht danach Vorhersagen.
Die Snake führt diese Vorhersage als Aktion aus.
```

## Das musst du nicht im Detail verstehen

```text
Backpropagation
Gewichtsmatrizen
MLPClassifier intern
Optimierungsverfahren
scikit-learn intern
```

Das ist in diesem Projekt Blackbox-Code.

Du darfst diesen Code benutzen.

Du musst ihn nicht vollständig erklären können.

# 2. Die drei Code-Arten

| Code-Art      | Bedeutung                 | Was du machst              |
| ------------- | ------------------------- | -------------------------- |
| Blackbox-Code | vorbereiteter Code        | ausführen, grob verstehen |
| Arbeits-Code  | kleine Funktionen         | lesen, ändern, testen     |
| Kreativ-Code  | Aussehen und Spielgefühl | selber gestalten           |

## Blackbox-Code

Diesen Code musst du nicht vollständig verstehen.

```text
train_model.py
engine/ai_player.py
engine/data_recorder.py
```

## Arbeits-Code

Diesen Code sollst du teilweise verstehen.

```text
student_tasks.py
engine/snake_logic.py
engine/features.py
tests/
```

## Kreativ-Code

Hier darfst du sichtbar etwas ändern.

```text
student_config.py
game.py
```

# 3. Zeitplan für 12 Lektionen

| Lektion | Ziel                                                | Ergebnis                      |
| ------: | --------------------------------------------------- | ----------------------------- |
|       1 | Projektordner und Dateien erstellen                 | Projektstruktur ist bereit    |
|       2 | virtuelle Umgebung einrichten                       | Pakete sind installiert       |
|       3 | Spiel starten und verstehen                         | Snake läuft                  |
|       4 | Aussehen ändern                                    | dein Spiel sieht anders aus   |
|       5 | kleine Funktionen in `student_tasks.py` verstehen | erste Tests laufen            |
|       6 | Tests ausführen und ergänzen                      | pytest ist grün              |
|       7 | Spielzustand als Zahlen verstehen                   | Features sind grob verstanden |
|       8 | Trainingsdaten anschauen                            | CSV-Datei ist verstanden      |
|       9 | Modell trainieren                                   | Modelldatei entsteht          |
|      10 | KI-Modus testen                                     | KI spielt selbst              |
|      11 | kleine Auswertung und Dokumentation                 | Tabelle und Reflexion         |
|      12 | Abgabe prüfen und verbessern                       | Projekt ist abgabebereit      |

# 4. Schritt 1: Ordnerstruktur erstellen

Erstelle zuerst einen Ordner mit dem Namen:

```text
snake_trainer
```

Öffne diesen Ordner in VS Code.

Erstelle dann diese Struktur:

```text
snake_trainer/
│
├── game.py
├── student_config.py
├── student_tasks.py
├── train_model.py
├── generate_training_data.py
├── requirements.txt
├── pytest.ini
├── README.md
│
├── engine/
│   ├── __init__.py
│   ├── snake_logic.py
│   ├── features.py
│   ├── data_recorder.py
│   └── ai_player.py
│
├── data/
│   └── example_training.csv
│
├── models/
│   └── .gitkeep
│
└── tests/
    ├── test_student_tasks.py
    ├── test_snake_logic.py
    ├── test_features.py
    ├── test_data_recorder.py
    └── test_ai_player.py
```

## Tipp

Du kannst die Ordner auch mit dem Terminal erstellen:

```bash
mkdir snake_trainer
cd snake_trainer
mkdir engine data models tests
```

Die Dateien erstellst du danach in VS Code.

# 5. Schritt 2: Dateien erstellen

Kopiere nun die folgenden Inhalte in die passenden Dateien.

## Datei: `pytest.ini`

```ini
[pytest]
pythonpath = .
testpaths = tests
```

## Was macht diese Datei?

Diese Datei sagt `pytest`, wo es suchen soll.

Die Zeile

```ini
pythonpath = .
```

bedeutet:

```text
Suche Python-Dateien auch im aktuellen Projektordner.
```

So findet Python zum Beispiel diese Dateien:

```text
student_config.py
student_tasks.py
engine/snake_logic.py
engine/features.py
```

Die Zeile

```ini
testpaths = tests
```

bedeutet:

```text
Die Tests liegen im Ordner tests.
```

`pytest` sucht also dort nach Testdateien.

Pflicht: ja
Schwierigkeit: leicht
Code verstehen: grob
Code ändern: nein

## Datei: `requirements.txt`

```text
pgzero
pygame
scikit-learn
pandas
joblib
pytest
pytest-cov
```

## Was macht diese Datei?

Diese Datei sagt Python, welche Pakete dein Projekt braucht.

Du musst den Inhalt nicht verändern.

Pflicht: ja
Schwierigkeit: leicht
Code verstehen: grob
Code ändern: nein

## Datei: `student_config.py`

```python
"""
Diese Datei darfst du verändern.

Hier kannst du das Aussehen und das Spielgefühl anpassen.
"""

# Spielfeld
GRID_WIDTH = 24
GRID_HEIGHT = 18
GRID_SIZE = 20

# Spielgeschwindigkeit
SNAKE_SPEED = 7

# Farben
BACKGROUND_COLOR = "black"
GRID_COLOR = "darkslategray"
SNAKE_COLOR = "green"
SNAKE_HEAD_COLOR = "lime"
FOOD_COLOR = "red"
TEXT_COLOR = "white"

# Texte
GAME_TITLE = "SnakeTrainer"
HUMAN_MODE_TEXT = "Modus: Mensch"
AI_MODE_TEXT = "Modus: KI"
GAME_OVER_TEXT = "Game Over - Drücke R für Neustart"

# KI
USE_AI_BY_DEFAULT = False

# Trainingsdaten
SAVE_HUMAN_DATA = True
TRAINING_DATA_PATH = "data/snake_training.csv"
FALLBACK_TRAINING_DATA_PATH = "data/example_training.csv"
MODEL_PATH = "models/snake_mlp.joblib"
```

## Was macht diese Datei?

Hier stehen einfache Einstellungen.

Du kannst hier gefahrlos Dinge ändern.

## TODOs in dieser Datei

| TODO | Aufgabe                                   | Pflicht?    | Schwierigkeit |
| ---- | ----------------------------------------- | ----------- | ------------- |
| C1   | Ändere mindestens drei Farben oder Texte | ja          | leicht        |
| C2   | Ändere die Spielgeschwindigkeit          | ja          | leicht        |
| C3   | Ändere den Spieltitel                    | Wahlaufgabe | leicht        |
| C4   | Ändere die Spielfeldgrösse              | Wahlaufgabe | mittel        |

## Was sollst du verstehen?

Du sollst verstehen:

```text
Wenn du hier Werte änderst, ändert sich das Spiel.
```

Du musst nicht verstehen, wie Pygame Zero diese Werte später zeichnet.

## Datei: `student_tasks.py`

```python
"""
In dieser Datei löst du kleine Programmieraufgaben.

Die Funktionen werden vom Spiel verwendet.
Du kannst sie mit pytest testen.
"""

from student_config import AI_MODE_TEXT, HUMAN_MODE_TEXT


def format_score(score):
    """
    Erstellt den Text für die Punkteanzeige.

    Beispiel:
        score = 5
        Rückgabe: "Score: 5"
    """
    # TODO PFLICHT LEICHT:
    # Verändere den Text, wenn du möchtest.
    # Beispiel: "Punkte: 5"
    return f"Score: {score}"


def format_high_score(high_score):
    """
    Erstellt den Text für den Highscore.

    Beispiel:
        high_score = 12
        Rückgabe: "Highscore: 12"
    """
    # TODO PFLICHT LEICHT:
    # Gib einen Text mit dem Highscore zurück.
    return f"Highscore: {high_score}"


def get_mode_text(ai_mode):
    """
    Erstellt den Text für den aktuellen Spielmodus.

    Args:
        ai_mode: True bedeutet KI-Modus.
        ai_mode: False bedeutet Mensch-Modus.
    """
    # TODO PFLICHT MITTEL:
    # Lies die if-Anweisung.
    # Erkläre in deiner Dokumentation, was hier passiert.
    if ai_mode:
        return AI_MODE_TEXT

    return HUMAN_MODE_TEXT


def is_high_score(score, high_score):
    """
    Prüft, ob ein neuer Highscore erreicht wurde.
    """
    # TODO PFLICHT LEICHT:
    # Diese Funktion soll True zurückgeben,
    # wenn score grösser ist als high_score.
    return score > high_score


def get_ai_status_text(model_loaded):
    """
    Erstellt eine kurze Meldung für den KI-Modus.
    """
    # TODO WAHL MITTEL:
    # Passe die Texte an.
    if model_loaded:
        return "KI-Modell geladen"

    return "Kein KI-Modell gefunden"
```

## Was macht diese Datei?

Hier sind kleine Funktionen.

Sie sind kurz.

Sie sind gut zum Üben.

## TODOs in dieser Datei

| TODO | Aufgabe                                        | Pflicht?    | Schwierigkeit |
| ---- | ---------------------------------------------- | ----------- | ------------- |
| T1   | Ändere den Score-Text                         | ja          | leicht        |
| T2   | Prüfe `is_high_score()` mit Tests           | ja          | leicht        |
| T3   | Erkläre `get_mode_text()` in eigenen Worten | ja          | mittel        |
| T4   | Ändere die KI-Meldung                         | Wahlaufgabe | mittel        |

## Was sollst du verstehen?

Du sollst diese Datei am besten verstehen.

Hier übst du:

```text
Funktionen
Parameter
return
if / else
Tests
```

## Datei: `engine/__init__.py`

```python
"""
Hilfsmodule für SnakeTrainer.
"""
```

## Was macht diese Datei?

Diese Datei macht aus dem Ordner `engine` ein Python-Paket.

Du musst hier nichts ändern.

Pflicht: nein
Schwierigkeit: leicht
Code verstehen: nein
Code ändern: nein

## Datei: `engine/snake_logic.py`

```python
"""
Reine Spiellogik für Snake.

Diese Datei zeichnet nichts auf den Bildschirm.
Sie berechnet nur Bewegung und Kollision.

Diese Datei ist Arbeits-Code.
Einige Funktionen sollst du grob verstehen.
"""

ACTION_LEFT = 0
ACTION_STRAIGHT = 1
ACTION_RIGHT = 2

DIRECTION_UP = (0, -1)
DIRECTION_DOWN = (0, 1)
DIRECTION_LEFT = (-1, 0)
DIRECTION_RIGHT = (1, 0)


def turn_direction(direction, action):
    """
    Berechnet die neue Richtung nach einer Aktion.

    Args:
        direction: aktuelle Richtung, zum Beispiel (1, 0)
        action: 0 = links, 1 = geradeaus, 2 = rechts
    """
    dx, dy = direction

    if action == ACTION_STRAIGHT:
        return direction

    if action == ACTION_LEFT:
        return (dy, -dx)

    if action == ACTION_RIGHT:
        return (-dy, dx)

    raise ValueError("Unbekannte Aktion")


def get_next_position(head, direction):
    """
    Berechnet die nächste Position des Snake-Kopfes.
    """
    return (head[0] + direction[0], head[1] + direction[1])


def is_collision(position, snake_body, grid_width, grid_height):
    """
    Prüft, ob eine Position mit Wand oder Körper kollidiert.
    """
    x, y = position

    if x < 0 or x >= grid_width:
        return True

    if y < 0 or y >= grid_height:
        return True

    if position in snake_body:
        return True

    return False


def get_relative_action(current_direction, desired_direction):
    """
    Wandelt eine gewünschte Richtung in eine relative Aktion um.

    Beispiel:
        aktuelle Richtung: rechts
        gewünschte Richtung: oben
        Ergebnis: links drehen
    """
    if desired_direction == current_direction:
        return ACTION_STRAIGHT

    if desired_direction == turn_direction(current_direction, ACTION_LEFT):
        return ACTION_LEFT

    if desired_direction == turn_direction(current_direction, ACTION_RIGHT):
        return ACTION_RIGHT

    # Eine direkte Umkehr ist bei Snake nicht erlaubt.
    return None
```

## Was macht diese Datei?

Diese Datei enthält die Grundregeln.

Beispiele:

```text
Wie dreht sich die Snake?
Wo ist die nächste Position?
Wann ist eine Kollision?
```

## TODOs in dieser Datei

| TODO | Aufgabe                                          | Pflicht?    | Schwierigkeit |
| ---- | ------------------------------------------------ | ----------- | ------------- |
| L1   | Lies `get_next_position()` und erkläre sie    | ja          | leicht        |
| L2   | Führe die Tests zu dieser Datei aus             | ja          | leicht        |
| L3   | Ergänze einen eigenen Test zu einer Wand        | ja          | mittel        |
| L4   | Erkläre `turn_direction()` mit einem Beispiel | Wahlaufgabe | mittel        |

## Was sollst du verstehen?

Du sollst verstehen:

```text
Eine Richtung ist ein Tupel.
(1, 0) bedeutet rechts.
(-1, 0) bedeutet links.
(0, -1) bedeutet oben.
(0, 1) bedeutet unten.
```

Du musst die Drehformeln nicht perfekt erklären können.

## Datei: `engine/features.py`

```python
"""
Feature-Extraktion für die Snake-KI.

Ein Modell kann nicht direkt mit dem ganzen Spiel arbeiten.
Darum wandeln wir den Spielzustand in Zahlen um.

Diese Zahlen nennt man Features.
"""

from engine.snake_logic import (
    ACTION_LEFT,
    ACTION_RIGHT,
    ACTION_STRAIGHT,
    get_next_position,
    is_collision,
    turn_direction,
)


FEATURE_NAMES = [
    "danger_front",
    "danger_left",
    "danger_right",
    "food_left",
    "food_right",
    "food_up",
    "food_down",
    "direction_up",
    "direction_down",
    "direction_left",
    "direction_right",
]


def extract_features(snake, direction, food, grid_width, grid_height):
    """
    Wandelt den aktuellen Spielzustand in eine Liste von Zahlen um.

    Jede Zahl ist 0 oder 1.
    """
    head = snake[0]
    body_without_head = snake[1:]

    front_direction = turn_direction(direction, ACTION_STRAIGHT)
    left_direction = turn_direction(direction, ACTION_LEFT)
    right_direction = turn_direction(direction, ACTION_RIGHT)

    front_position = get_next_position(head, front_direction)
    left_position = get_next_position(head, left_direction)
    right_position = get_next_position(head, right_direction)

    danger_front = int(is_collision(front_position, body_without_head, grid_width, grid_height))
    danger_left = int(is_collision(left_position, body_without_head, grid_width, grid_height))
    danger_right = int(is_collision(right_position, body_without_head, grid_width, grid_height))

    food_left = int(food[0] < head[0])
    food_right = int(food[0] > head[0])
    food_up = int(food[1] < head[1])
    food_down = int(food[1] > head[1])

    direction_up = int(direction == (0, -1))
    direction_down = int(direction == (0, 1))
    direction_left = int(direction == (-1, 0))
    direction_right = int(direction == (1, 0))

    return [
        danger_front,
        danger_left,
        danger_right,
        food_left,
        food_right,
        food_up,
        food_down,
        direction_up,
        direction_down,
        direction_left,
        direction_right,
    ]
```

## Was macht diese Datei?

Diese Datei ist die Brücke zur KI.

Das Spiel hat viele Informationen.

Das Modell braucht aber Zahlen.

Beispiel:

```python
[0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1]
```

Das kann bedeuten:

```text
vorne keine Gefahr
links Gefahr
rechts keine Gefahr
Futter rechts
Snake bewegt sich nach rechts
```

## TODOs in dieser Datei

| TODO | Aufgabe                                              | Pflicht?    | Schwierigkeit |
| ---- | ---------------------------------------------------- | ----------- | ------------- |
| F1   | Führe die Feature-Tests aus                         | ja          | leicht        |
| F2   | Erkläre 3 Features in eigenen Worten                | ja          | mittel        |
| F3   | Ergänze einen Test zu `food_left`oder `food_up` | ja          | mittel        |
| F4   | Neues Feature ergänzen                              | Wahlaufgabe | anspruchsvoll |

## Was sollst du verstehen?

Du sollst verstehen:

```text
Die KI sieht nicht das Spielfeld.
Die KI sieht nur Zahlen.
Diese Zahlen beschreiben die Situation.
```

Du musst nicht alle Details der Funktion auswendig erklären.

## Datei: `engine/data_recorder.py`

```python
"""
Speichern von Trainingsdaten.

Diese Datei schreibt Spielzustände und Aktionen in eine CSV-Datei.
Damit kann später ein Modell trainiert werden.

Diese Datei ist Blackbox-Code.
Du darfst sie benutzen.
Du musst sie nicht vollständig verstehen.
"""

import csv
import os

from engine.features import FEATURE_NAMES
from engine.snake_logic import ACTION_LEFT, ACTION_RIGHT, ACTION_STRAIGHT
from student_config import TRAINING_DATA_PATH


CSV_HEADER = FEATURE_NAMES + ["action"]
ALLOWED_ACTIONS = [ACTION_LEFT, ACTION_STRAIGHT, ACTION_RIGHT]


def ensure_data_file(data_path=TRAINING_DATA_PATH):
    """
    Erstellt die Trainingsdatei, falls sie noch nicht existiert.
    """
    folder = os.path.dirname(data_path)

    if folder and not os.path.exists(folder):
        os.makedirs(folder)

    if os.path.exists(data_path):
        return

    with open(data_path, "w", newline="", encoding="utf-8") as csv_file:
        writer = csv.writer(csv_file)
        writer.writerow(CSV_HEADER)


def save_training_row(features, action, data_path=TRAINING_DATA_PATH):
    """
    Speichert eine einzelne Trainingszeile.
    """
    if len(features) != len(FEATURE_NAMES):
        raise ValueError("Die Anzahl der Features stimmt nicht.")

    if action not in ALLOWED_ACTIONS:
        raise ValueError("Die Aktion ist ungültig.")

    ensure_data_file(data_path)

    row = list(features) + [action]

    with open(data_path, "a", newline="", encoding="utf-8") as csv_file:
        writer = csv.writer(csv_file)
        writer.writerow(row)
```

## Was macht diese Datei?

Diese Datei speichert Trainingsdaten.

Eine Zeile besteht aus:

```text
Features + Aktion
```

## TODOs in dieser Datei

| TODO | Aufgabe                                             | Pflicht?    | Schwierigkeit |
| ---- | --------------------------------------------------- | ----------- | ------------- |
| D1   | Öffne später `data/snake_training.csv`          | ja          | leicht        |
| D2   | Erkläre, was die letzte Spalte `action` bedeutet | ja          | leicht        |
| D3   | Teste das Speichern mit pytest                      | Wahlaufgabe | mittel        |

## Was sollst du verstehen?

Du sollst verstehen:

```text
Diese Datei sammelt Beispiele.
Diese Beispiele braucht das Modell zum Lernen.
```

Du musst die Datei nicht vollständig erklären.

## Datei: `engine/ai_player.py`

```python
"""
KI-Spieler für Snake.

Diese Datei lädt ein trainiertes Modell.
Danach fragt sie das Modell nach einer Aktion.

Diese Datei ist Blackbox-Code.
"""

import os

import joblib

from engine.snake_logic import ACTION_LEFT, ACTION_RIGHT, ACTION_STRAIGHT
from student_config import MODEL_PATH


ALLOWED_ACTIONS = [ACTION_LEFT, ACTION_STRAIGHT, ACTION_RIGHT]


def load_model(model_path=MODEL_PATH):
    """
    Lädt ein trainiertes Modell.

    Wenn kein Modell gefunden wird, gibt die Funktion None zurück.
    """
    if not os.path.exists(model_path):
        return None

    return joblib.load(model_path)


def predict_action(model, features):
    """
    Fragt das Modell nach der nächsten Aktion.

    Rückgabe:
        0 = links
        1 = geradeaus
        2 = rechts
    """
    if model is None:
        return ACTION_STRAIGHT

    prediction = model.predict([features])[0]
    action = int(prediction)

    if action not in ALLOWED_ACTIONS:
        return ACTION_STRAIGHT

    return action
```

## Was macht diese Datei?

Diese Datei fragt die KI:

```text
Was soll die Snake jetzt tun?
```

Dann kommt eine Zahl zurück:

```text
0 = links
1 = geradeaus
2 = rechts
```

## TODOs in dieser Datei

| TODO | Aufgabe                                     | Pflicht?    | Schwierigkeit |
| ---- | ------------------------------------------- | ----------- | ------------- |
| A1   | Starte später den KI-Modus                 | ja          | leicht        |
| A2   | Erkläre `predict_action()` in einem Satz | ja          | mittel        |
| A3   | Ergänze einen FakeModel-Test               | Wahlaufgabe | mittel        |

## Was sollst du verstehen?

Du sollst verstehen:

```text
Das Modell gibt eine Aktion zurück.
Das Spiel führt diese Aktion aus.
```

Du musst `joblib` und `model.predict()` nicht im Detail verstehen.

## Datei: `train_model.py`

```python
"""
Training des KI-Modells.

Diese Datei liest Trainingsdaten aus einer CSV-Datei.
Danach wird ein kleines neuronales Netz trainiert.

Diese Datei ist fast vollständig Blackbox-Code.
Du führst sie aus.
Du darfst einzelne Werte ändern, wenn du eine Wahlaufgabe machst.
"""

import os

import joblib
import pandas as pd

from sklearn.metrics import accuracy_score
from sklearn.model_selection import train_test_split
from sklearn.neural_network import MLPClassifier

from engine.features import FEATURE_NAMES
from student_config import (
    FALLBACK_TRAINING_DATA_PATH,
    MODEL_PATH,
    TRAINING_DATA_PATH,
)


def choose_data_path():
    """
    Wählt die passende Trainingsdatei.

    Wenn eigene Trainingsdaten vorhanden sind, werden diese genutzt.
    Sonst wird die Beispieldatei verwendet.
    """
    if os.path.exists(TRAINING_DATA_PATH):
        data = pd.read_csv(TRAINING_DATA_PATH)

        if len(data) >= 8:
            return TRAINING_DATA_PATH

    return FALLBACK_TRAINING_DATA_PATH


def train_model(data_path=None, model_path=MODEL_PATH):
    """
    Trainiert ein MLP-Modell mit Snake-Daten.
    """
    if data_path is None:
        data_path = choose_data_path()

    if not os.path.exists(data_path):
        raise FileNotFoundError("Keine Trainingsdatei gefunden.")

    data = pd.read_csv(data_path)

    if len(data) < 8:
        raise ValueError("Es sind zu wenige Trainingsdaten vorhanden.")

    required_columns = FEATURE_NAMES + ["action"]

    for column in required_columns:
        if column not in data.columns:
            raise ValueError(f"Spalte fehlt: {column}")

    x_values = data[FEATURE_NAMES]
    y_values = data["action"]

    if len(data) >= 12:
        x_train, x_test, y_train, y_test = train_test_split(
            x_values,
            y_values,
            test_size=0.25,
            random_state=42,
        )
    else:
        x_train = x_values
        x_test = x_values
        y_train = y_values
        y_test = y_values

    # TODO WAHL MITTEL:
    # Du darfst hidden_layer_sizes verändern.
    # Beispiel: (8,), (12,), (20,), (12, 6)
    model = MLPClassifier(
        hidden_layer_sizes=(12,),
        activation="relu",
        max_iter=1000,
        random_state=42,
    )

    model.fit(x_train, y_train)

    predictions = model.predict(x_test)
    accuracy = accuracy_score(y_test, predictions)

    model_folder = os.path.dirname(model_path)

    if model_folder and not os.path.exists(model_folder):
        os.makedirs(model_folder)

    joblib.dump(model, model_path)

    print(f"Verwendete Trainingsdatei: {data_path}")
    print(f"Trainingszeilen: {len(data)}")
    print(f"Testgenauigkeit: {accuracy:.2f}")
    print(f"Modell gespeichert unter: {model_path}")

    return accuracy


if __name__ == "__main__":
    train_model()
```

## Was macht diese Datei?

Diese Datei trainiert die KI.

Ablauf:

```text
CSV-Datei laden
Features und Aktionen trennen
Modell trainieren
Modell testen
Modell speichern
```

## TODOs in dieser Datei

| TODO | Aufgabe                                         | Pflicht?    | Schwierigkeit |
| ---- | ----------------------------------------------- | ----------- | ------------- |
| M1   | Führe `python train_model.py` aus            | ja          | leicht        |
| M2   | Prüfe, ob `models/snake_mlp.joblib` entsteht | ja          | leicht        |
| M3   | Erkläre `fit()` in einem Satz                | ja          | mittel        |
| M4   | Ändere `hidden_layer_sizes`                  | Wahlaufgabe | mittel        |

## Was sollst du verstehen?

Du sollst verstehen:

```text
fit() bedeutet: Das Modell lernt aus Beispielen.
predict() bedeutet: Das Modell macht eine Vorhersage.
```

Du musst nicht verstehen, wie das neuronale Netz intern lernt.

## Datei: `tests/test_snake_logic.py`

```python
import pytest

from engine.snake_logic import (
    ACTION_LEFT,
    ACTION_RIGHT,
    ACTION_STRAIGHT,
    DIRECTION_RIGHT,
    DIRECTION_UP,
    get_next_position,
    get_relative_action,
    is_collision,
    turn_direction,
)


def test_turn_direction_straight():
    assert turn_direction((1, 0), ACTION_STRAIGHT) == (1, 0)


def test_turn_direction_left_from_right():
    assert turn_direction((1, 0), ACTION_LEFT) == (0, -1)


def test_turn_direction_right_from_right():
    assert turn_direction((1, 0), ACTION_RIGHT) == (0, 1)


def test_turn_direction_invalid_action():
    with pytest.raises(ValueError):
        turn_direction((1, 0), 99)


def test_get_next_position():
    assert get_next_position((5, 5), (1, 0)) == (6, 5)


def test_collision_with_left_wall():
    assert is_collision((-1, 5), [], 24, 18) is True


def test_collision_with_body():
    body = [(5, 5), (6, 5)]
    assert is_collision((5, 5), body, 24, 18) is True


def test_no_collision():
    body = [(5, 5), (6, 5)]
    assert is_collision((7, 5), body, 24, 18) is False


def test_get_relative_action_left():
    assert get_relative_action(DIRECTION_RIGHT, DIRECTION_UP) == ACTION_LEFT
```

## Datei: `generate_training_data.py`

```python
"""
Erzeugt Trainingsdaten für SnakeTrainer.

Diese Datei ist Blackbox-Code.

Sie erstellt viele Beispiele für die KI.
Ein einfacher Regel-Lehrer entscheidet:

1. Nicht in eine Wand oder in den Körper fahren.
2. Möglichst in Richtung Futter gehen.
3. Wenn mehrere Aktionen möglich sind, wird eine gute Aktion gewählt.

Die erzeugten Daten werden in data/snake_training.csv gespeichert.
Danach kann das Modell mit train_model.py trainiert werden.

Wichtig:
Diese Datei überschreibt data/snake_training.csv.
"""

import csv
import os
import random
from collections import Counter

from engine.features import FEATURE_NAMES
from engine.snake_logic import (
    ACTION_LEFT,
    ACTION_RIGHT,
    ACTION_STRAIGHT,
    DIRECTION_DOWN,
    DIRECTION_LEFT,
    DIRECTION_RIGHT,
    DIRECTION_UP,
    turn_direction,
)
from student_config import TRAINING_DATA_PATH


ROWS_PER_PATTERN = 20
RANDOM_SEED = 42

ACTIONS = [ACTION_LEFT, ACTION_STRAIGHT, ACTION_RIGHT]
DIRECTIONS = [DIRECTION_UP, DIRECTION_DOWN, DIRECTION_LEFT, DIRECTION_RIGHT]

ACTION_NAMES = {
    ACTION_LEFT: "links",
    ACTION_STRAIGHT: "geradeaus",
    ACTION_RIGHT: "rechts",
}


def get_direction_features(direction):
    """
    Wandelt eine Richtung in vier Zahlen um.

    Beispiel:
        Richtung rechts = [0, 0, 0, 1]
    """
    direction_up = int(direction == DIRECTION_UP)
    direction_down = int(direction == DIRECTION_DOWN)
    direction_left = int(direction == DIRECTION_LEFT)
    direction_right = int(direction == DIRECTION_RIGHT)

    return [
        direction_up,
        direction_down,
        direction_left,
        direction_right,
    ]


def get_food_relations():
    """
    Erstellt mögliche Positionen des Futters relativ zur Snake.

    Das Futter kann links, rechts, oben oder unten liegen.
    Es kann auch diagonal liegen.
    """
    x_relations = [
        (1, 0),  # Futter links
        (0, 0),  # gleiche Spalte
        (0, 1),  # Futter rechts
    ]

    y_relations = [
        (1, 0),  # Futter oben
        (0, 0),  # gleiche Zeile
        (0, 1),  # Futter unten
    ]

    relations = []

    for food_left, food_right in x_relations:
        for food_up, food_down in y_relations:
            # Das Futter soll nicht genau auf dem Kopf liegen.
            if food_left == 0 and food_right == 0 and food_up == 0 and food_down == 0:
                continue

            relations.append(
                (food_left, food_right, food_up, food_down)
            )

    return relations


def get_danger_patterns():
    """
    Erstellt alle Kombinationen von Gefahr vorne, links und rechts.
    """
    patterns = []

    for danger_front in [0, 1]:
        for danger_left in [0, 1]:
            for danger_right in [0, 1]:
                patterns.append(
                    (danger_front, danger_left, danger_right)
                )

    return patterns


def score_direction(new_direction, food_left, food_right, food_up, food_down):
    """
    Bewertet, ob eine Richtung zum Futter passt.

    Hohe Punktzahl bedeutet:
        Diese Richtung ist gut.

    Tiefe Punktzahl bedeutet:
        Diese Richtung geht eher vom Futter weg.
    """
    dx, dy = new_direction
    score = 0

    if food_right:
        if dx == 1:
            score += 3
        elif dx == -1:
            score -= 2

    if food_left:
        if dx == -1:
            score += 3
        elif dx == 1:
            score -= 2

    if food_down:
        if dy == 1:
            score += 3
        elif dy == -1:
            score -= 2

    if food_up:
        if dy == -1:
            score += 3
        elif dy == 1:
            score -= 2

    return score


def choose_teacher_action(
    direction,
    danger_front,
    danger_left,
    danger_right,
    food_left,
    food_right,
    food_up,
    food_down,
):
    """
    Wählt eine gute Aktion für einen Spielzustand.

    Diese Funktion ist der Regel-Lehrer.
    Er erzeugt die richtige Antwort für die Trainingsdaten.
    """
    danger_by_action = {
        ACTION_STRAIGHT: danger_front,
        ACTION_LEFT: danger_left,
        ACTION_RIGHT: danger_right,
    }

    safe_actions = []

    for action in ACTIONS:
        if danger_by_action[action] == 0:
            safe_actions.append(action)

    # Wenn alles gefährlich ist, gibt es keine gute Lösung mehr.
    # Dann nehmen wir geradeaus als Notfallwert.
    if not safe_actions:
        return ACTION_STRAIGHT

    best_action = safe_actions[0]
    best_score = -999

    for action in safe_actions:
        new_direction = turn_direction(direction, action)

        score = score_direction(
            new_direction,
            food_left,
            food_right,
            food_up,
            food_down,
        )

        # Kleine Bevorzugung für geradeaus.
        # Dadurch fährt die Snake ruhiger, wenn es sinnvoll ist.
        if action == ACTION_STRAIGHT:
            score += 0.2

        # Kleine zufällige Variation.
        # Dadurch entstehen nicht immer exakt gleiche Muster.
        score += random.random() * 0.01

        if score > best_score:
            best_score = score
            best_action = action

    return best_action


def create_feature_row(
    direction,
    danger_front,
    danger_left,
    danger_right,
    food_left,
    food_right,
    food_up,
    food_down,
):
    """
    Erstellt eine Feature-Zeile im gleichen Format wie features.py.
    """
    direction_features = get_direction_features(direction)

    return [
        danger_front,
        danger_left,
        danger_right,
        food_left,
        food_right,
        food_up,
        food_down,
    ] + direction_features


def generate_rows():
    """
    Erstellt viele Trainingszeilen.
    """
    rows = []
    food_relations = get_food_relations()
    danger_patterns = get_danger_patterns()

    for direction in DIRECTIONS:
        for danger_front, danger_left, danger_right in danger_patterns:
            for food_left, food_right, food_up, food_down in food_relations:
                features = create_feature_row(
                    direction,
                    danger_front,
                    danger_left,
                    danger_right,
                    food_left,
                    food_right,
                    food_up,
                    food_down,
                )

                action = choose_teacher_action(
                    direction,
                    danger_front,
                    danger_left,
                    danger_right,
                    food_left,
                    food_right,
                    food_up,
                    food_down,
                )

                row = features + [action]

                for _ in range(ROWS_PER_PATTERN):
                    rows.append(row)

    random.shuffle(rows)
    return rows


def write_csv(rows, data_path):
    """
    Speichert die erzeugten Trainingsdaten als CSV-Datei.
    """
    folder = os.path.dirname(data_path)

    if folder and not os.path.exists(folder):
        os.makedirs(folder)

    header = FEATURE_NAMES + ["action"]

    with open(data_path, "w", newline="", encoding="utf-8") as csv_file:
        writer = csv.writer(csv_file)
        writer.writerow(header)
        writer.writerows(rows)


def print_summary(rows):
    """
    Gibt eine kurze Zusammenfassung aus.
    """
    action_counter = Counter(row[-1] for row in rows)

    print("Trainingsdaten erzeugt")
    print(f"Anzahl Zeilen: {len(rows)}")
    print()

    for action in ACTIONS:
        count = action_counter[action]
        name = ACTION_NAMES[action]
        print(f"Aktion {action} ({name}): {count}")

    print()
    print(f"Gespeichert unter: {TRAINING_DATA_PATH}")


def main():
    """
    Hauptprogramm.
    """
    random.seed(RANDOM_SEED)

    rows = generate_rows()
    write_csv(rows, TRAINING_DATA_PATH)
    print_summary(rows)


if __name__ == "__main__":
    main()
```

## Was macht diese Datei?

Diese Datei erzeugt automatisch Trainingsdaten für die KI.

Die KI braucht Beispiele.
Ohne gute Beispiele lernt sie schlecht.
Dann fährt sie vielleicht direkt in die Wand oder immer im Kreis.

Diese Datei erstellt viele künstliche Beispiele.
Ein einfacher Regel-Lehrer entscheidet, welche Aktion sinnvoll ist.

Ablauf:

```text
mögliche Spielzustände erstellen
prüfen, wo Gefahr ist
prüfen, wo das Futter liegt
eine gute Aktion wählen
Trainingsdaten als CSV speichern
```

Die Daten werden hier gespeichert:

```text
data/snake_training.csv
```

Danach musst du das Modell neu trainieren:

```bash
python train_model.py
```

Erst dann verwendet das Spiel die neuen Daten.

## Wichtig

Diese Datei überschreibt:

```text
data/snake_training.csv
```

Wenn du eigene Trainingsdaten gesammelt hast, können sie dadurch ersetzt werden.

Wenn du eigene Daten behalten möchtest, mache vorher eine Kopie.

Beispiel:

```text
data/snake_training_meine_daten.csv
```

## Wie verwendest du diese Datei?

Führe zuerst aus:

```bash
python generate_training_data.py
```

Danach:

```bash
python train_model.py
```

Dann:

```bash
pgzrun game.py
```

Im Spiel kannst du mit `K` den KI-Modus aktivieren.

## TODOs in dieser Datei

| TODO | Aufgabe                                                            | Pflicht?    | Schwierigkeit |
| ---- | ------------------------------------------------------------------ | ----------- | ------------- |
| G1   | Führe `python generate_training_data.py` aus                    | ja          | leicht        |
| G2   | Prüfe, ob `data/snake_training.csv` entsteht                    | ja          | leicht        |
| G3   | Öffne `data/snake_training.csv` und suche die Spalte `action` | ja          | leicht        |
| G4   | Erkläre in einem Satz, was der Regel-Lehrer macht                 | ja          | mittel        |
| G5   | Führe danach `python train_model.py` aus                        | ja          | leicht        |
| G6   | Teste den KI-Modus im Spiel mit der Taste `K`                    | ja          | leicht        |
| G7   | Ändere `ROWS_PER_PATTERN` und erzeuge neue Daten                | Wahlaufgabe | mittel        |
| G8   | Erkläre, warum neue Trainingsdaten ein neues Training brauchen    | Wahlaufgabe | mittel        |

## Was sollst du verstehen?

Du sollst verstehen:

```text
Eine KI braucht Beispiele.
Diese Datei erzeugt solche Beispiele automatisch.
Die Beispiele werden in einer CSV-Datei gespeichert.
train_model.py lernt danach aus dieser CSV-Datei.
```

Du musst nicht jede Zeile verstehen.

Du sollst aber diesen Ablauf erklären können:

```text
generate_training_data.py erzeugt Daten.
train_model.py trainiert das Modell.
game.py benutzt das Modell im KI-Modus.
```

## Was musst du nicht verstehen?

Du musst nicht vollständig verstehen:

```text
Counter
random.seed()
verschachtelte for-Schleifen
alle möglichen Gefahr-Muster
alle möglichen Futter-Positionen
```

Das ist Blackbox-Code.

## Was ist der Regel-Lehrer?

Der Regel-Lehrer ist keine echte KI.

Er ist ein einfacher Algorithmus.

Er entscheidet nach einfachen Regeln:

```text
Wenn vorne Gefahr ist, fahre nicht geradeaus.
Wenn links frei und sinnvoll ist, fahre links.
Wenn rechts frei und sinnvoll ist, fahre rechts.
Wenn geradeaus sicher und sinnvoll ist, fahre geradeaus.
```

Diese Entscheidungen werden als Trainingsdaten gespeichert.

Das Modell lernt danach aus diesen Entscheidungen.

## Warum ist diese Datei hilfreich?

Am Anfang hast du wenig Daten.

Mit wenig Daten spielt die KI schlecht.

Diese Datei gibt dir gute Startdaten.

Danach kann die KI besser lernen.

## Pflichtabgabe

Für die Abgabe brauchst du:

```text
Screenshot oder Textausgabe von:
python generate_training_data.py
```

und:

```text
Nachweis, dass data/snake_training.csv erzeugt wurde.
```

Zusätzlich brauchst du danach:

```text
Screenshot oder Textausgabe von:
python train_model.py
```

## Kurzer Merksatz

```text
generate_training_data.py erstellt Beispiele.
train_model.py lernt aus Beispielen.
game.py verwendet das Gelernte.
```

## Datei: `game.py`

```python
"""
SnakeTrainer-Spiel mit Pygame Zero.

Diese Datei zeigt das Spiel an.
Hier wird die Spiellogik mit der KI verbunden.

Du darfst hier kleine sichtbare Änderungen machen.
"""

import random

from pygame import Rect

from engine.ai_player import load_model, predict_action
from engine.data_recorder import save_training_row
from engine.features import extract_features
from engine.snake_logic import (
    ACTION_STRAIGHT,
    DIRECTION_DOWN,
    DIRECTION_LEFT,
    DIRECTION_RIGHT,
    DIRECTION_UP,
    get_next_position,
    get_relative_action,
    is_collision,
    turn_direction,
)
from student_config import (
    BACKGROUND_COLOR,
    FOOD_COLOR,
    GAME_OVER_TEXT,
    GAME_TITLE,
    GRID_COLOR,
    GRID_HEIGHT,
    GRID_SIZE,
    GRID_WIDTH,
    SAVE_HUMAN_DATA,
    SNAKE_COLOR,
    SNAKE_HEAD_COLOR,
    SNAKE_SPEED,
    TEXT_COLOR,
    USE_AI_BY_DEFAULT,
)
from student_tasks import (
    format_high_score,
    format_score,
    get_ai_status_text,
    get_mode_text,
    is_high_score,
)


WIDTH = GRID_WIDTH * GRID_SIZE
HEIGHT = GRID_HEIGHT * GRID_SIZE
TITLE = GAME_TITLE


snake = []
direction = DIRECTION_RIGHT
food = (0, 0)

score = 0
high_score = 0

game_over = False
ai_mode = USE_AI_BY_DEFAULT
model = load_model()

move_timer = 0
pending_action = ACTION_STRAIGHT
status_message = "Pfeiltasten: bewegen | K: KI | R: Neustart"


def create_food():
    """
    Sucht ein freies Feld für das Futter.
    """
    free_positions = []

    for x in range(GRID_WIDTH):
        for y in range(GRID_HEIGHT):
            position = (x, y)

            if position not in snake:
                free_positions.append(position)

    if not free_positions:
        return (0, 0)

    return random.choice(free_positions)


def reset_game():
    """
    Startet eine neue Runde.
    """
    global snake
    global direction
    global food
    global score
    global game_over
    global move_timer
    global pending_action
    global status_message

    center_x = GRID_WIDTH // 2
    center_y = GRID_HEIGHT // 2

    snake = [
        (center_x, center_y),
        (center_x - 1, center_y),
        (center_x - 2, center_y),
    ]

    direction = DIRECTION_RIGHT
    food = create_food()

    score = 0
    game_over = False
    move_timer = 0
    pending_action = ACTION_STRAIGHT
    status_message = "Neue Runde gestartet"


def draw_cell(position, color):
    """
    Zeichnet ein einzelnes Rasterfeld.
    """
    left = position[0] * GRID_SIZE
    top = position[1] * GRID_SIZE

    screen.draw.filled_rect(
        Rect((left, top), (GRID_SIZE - 1, GRID_SIZE - 1)),
        color,
    )


def draw_grid():
    """
    Zeichnet ein einfaches Raster.
    """
    for x in range(0, WIDTH, GRID_SIZE):
        screen.draw.line((x, 0), (x, HEIGHT), GRID_COLOR)

    for y in range(0, HEIGHT, GRID_SIZE):
        screen.draw.line((0, y), (WIDTH, y), GRID_COLOR)


def draw():
    """
    Zeichnet das Spiel.
    Diese Funktion wird von Pygame Zero automatisch aufgerufen.
    """
    screen.clear()
    screen.fill(BACKGROUND_COLOR)

    draw_grid()

    draw_cell(food, FOOD_COLOR)

    for index, part in enumerate(snake):
        if index == 0:
            draw_cell(part, SNAKE_HEAD_COLOR)
        else:
            draw_cell(part, SNAKE_COLOR)

    screen.draw.text(
        format_score(score),
        (10, 10),
        color=TEXT_COLOR,
        fontsize=28,
    )

    screen.draw.text(
        format_high_score(high_score),
        (10, 40),
        color=TEXT_COLOR,
        fontsize=24,
    )

    screen.draw.text(
        get_mode_text(ai_mode),
        (10, 68),
        color=TEXT_COLOR,
        fontsize=24,
    )

    screen.draw.text(
        status_message,
        (10, HEIGHT - 30),
        color=TEXT_COLOR,
        fontsize=20,
    )

    if game_over:
        screen.draw.text(
            GAME_OVER_TEXT,
            center=(WIDTH // 2, HEIGHT // 2),
            color=TEXT_COLOR,
            fontsize=36,
        )


def move_one_step():
    """
    Führt einen Spielschritt aus.
    """
    global snake
    global direction
    global food
    global score
    global high_score
    global game_over
    global pending_action
    global status_message

    if game_over:
        return

    features = extract_features(snake, direction, food, GRID_WIDTH, GRID_HEIGHT)

    if ai_mode:
        action = predict_action(model, features)
    else:
        action = pending_action

        if SAVE_HUMAN_DATA:
            save_training_row(features, action)

    pending_action = ACTION_STRAIGHT

    new_direction = turn_direction(direction, action)
    new_head = get_next_position(snake[0], new_direction)

    if is_collision(new_head, snake[1:], GRID_WIDTH, GRID_HEIGHT):
        game_over = True

        if is_high_score(score, high_score):
            high_score = score

        status_message = "Kollision"
        return

    direction = new_direction

    if new_head == food:
        snake = [new_head] + snake
        score += 1
        food = create_food()

        if is_high_score(score, high_score):
            high_score = score
    else:
        snake = [new_head] + snake[:-1]


def update(dt):
    """
    Aktualisiert das Spiel.
    Diese Funktion wird von Pygame Zero automatisch aufgerufen.
    """
    global move_timer

    if game_over:
        return

    move_timer += dt

    if move_timer >= 1 / SNAKE_SPEED:
        move_timer = 0
        move_one_step()


def on_key_down(key):
    """
    Reagiert auf Tasteneingaben.
    """
    global ai_mode
    global model
    global pending_action
    global status_message

    if key == keys.R:
        reset_game()
        return

    if key == keys.K:
        ai_mode = not ai_mode

        if ai_mode:
            model = load_model()
            status_message = get_ai_status_text(model is not None)
        else:
            status_message = "Mensch-Modus aktiv"

        return

    if ai_mode or game_over:
        return

    desired_direction = None

    if key == keys.UP:
        desired_direction = DIRECTION_UP

    if key == keys.DOWN:
        desired_direction = DIRECTION_DOWN

    if key == keys.LEFT:
        desired_direction = DIRECTION_LEFT

    if key == keys.RIGHT:
        desired_direction = DIRECTION_RIGHT

    if desired_direction is None:
        return

    action = get_relative_action(direction, desired_direction)

    if action is not None:
        pending_action = action


reset_game()
```

## Was macht diese Datei?

Diese Datei ist die sichtbare Bühne.

Hier siehst du:

```text
Snake
Futter
Score
Modus
Game Over
```

## TODOs in dieser Datei

| TODO | Aufgabe                                 | Pflicht?    | Schwierigkeit |
| ---- | --------------------------------------- | ----------- | ------------- |
| G1   | Starte das Spiel mit `pgzrun game.py` | ja          | leicht        |
| G2   | Spiele im Mensch-Modus                  | ja          | leicht        |
| G3   | Aktiviere den KI-Modus mit K            | ja          | leicht        |
| G4   | Ändere einen Text oder eine Farbe      | ja          | leicht        |
| G5   | Erkläre, was R und K machen            | ja          | leicht        |
| G6   | Zeige einen eigenen Zusatztext an       | Wahlaufgabe | mittel        |

## Was sollst du verstehen?

Du sollst verstehen:

```text
draw() zeichnet das Spiel.
update() bewegt das Spiel.
on_key_down() reagiert auf Tasten.
```

Du musst nicht jede Zeile in `game.py` verstehen.

## Datei: `data/example_training.csv`

```csv
danger_front,danger_left,danger_right,food_left,food_right,food_up,food_down,direction_up,direction_down,direction_left,direction_right,action
0,1,0,0,1,0,0,0,0,0,1,1
1,0,0,0,1,0,0,0,0,0,1,0
0,0,1,1,0,0,0,0,0,0,1,1
0,0,0,0,0,1,0,0,0,0,1,0
0,1,0,0,0,0,1,1,0,0,0,1
1,0,0,1,0,0,0,1,0,0,0,2
0,0,1,0,1,0,0,0,1,0,0,0
0,0,0,1,0,1,0,0,1,0,0,2
1,0,0,0,0,1,0,0,0,1,0,2
0,1,0,0,0,0,1,0,0,1,0,1
0,0,1,0,1,1,0,0,0,1,0,0
0,0,0,1,0,0,1,0,0,1,0,2
0,1,0,0,1,0,0,0,1,0,0,1
1,0,0,0,1,0,0,0,1,0,0,0
0,0,1,1,0,0,0,1,0,0,0,1
0,0,0,0,1,0,1,1,0,0,0,2
```

## Was macht diese Datei?

Das sind Beispiel-Daten.

Sie sind nicht perfekt.

Sie helfen nur beim ersten Test.

## TODOs in dieser Datei

| TODO | Aufgabe                               | Pflicht?    | Schwierigkeit |
| ---- | ------------------------------------- | ----------- | ------------- |
| CSV1 | Öffne die Datei                      | ja          | leicht        |
| CSV2 | Finde die Spalte `action`           | ja          | leicht        |
| CSV3 | Erkläre eine Zeile in eigenen Worten | ja          | mittel        |
| CSV4 | Sammle eigene Daten im Spiel          | Wahlaufgabe | mittel        |

## Datei: `tests/test_student_tasks.py`

```python
from student_config import AI_MODE_TEXT, HUMAN_MODE_TEXT
from student_tasks import (
    format_high_score,
    format_score,
    get_mode_text,
    is_high_score,
)


def test_format_score():
    assert "5" in format_score(5)


def test_format_high_score():
    assert "12" in format_high_score(12)


def test_get_mode_text_ai():
    assert get_mode_text(True) == AI_MODE_TEXT


def test_get_mode_text_human():
    assert get_mode_text(False) == HUMAN_MODE_TEXT


def test_is_high_score_true():
    assert is_high_score(10, 5) is True


def test_is_high_score_false():
    assert is_high_score(3, 5) is False
```

## Was macht diese Datei?

Diese Tests prüfen deine einfachen Funktionen.

Pflicht: ja
Schwierigkeit: leicht bis mittel
Code verstehen: ja
Code ändern: ja

## Datei: `tests/test_snake_logic.py`

```python
import pytest

from engine.snake_logic import (
    ACTION_LEFT,
    ACTION_RIGHT,
    ACTION_STRAIGHT,
    DIRECTION_RIGHT,
    DIRECTION_UP,
    get_next_position,
    get_relative_action,
    is_collision,
    turn_direction,
)


def test_turn_direction_straight():
    assert turn_direction((1, 0), ACTION_STRAIGHT) == (1, 0)


def test_turn_direction_left_from_right():
    assert turn_direction((1, 0), ACTION_LEFT) == (0, -1)


def test_turn_direction_right_from_right():
    assert turn_direction((1, 0), ACTION_RIGHT) == (0, 1)


def test_turn_direction_invalid_action():
    with pytest.raises(ValueError):
        turn_direction((1, 0), 99)


def test_get_next_position():
    assert get_next_position((5, 5), (1, 0)) == (6, 5)


def test_collision_with_left_wall():
    assert is_collision((-1, 5), [], 24, 18) is True


def test_collision_with_body():
    body = [(5, 5), (6, 5)]
    assert is_collision((5, 5), body, 24, 18) is True


def test_no_collision():
    body = [(5, 5), (6, 5)]
    assert is_collision((7, 5), body, 24, 18) is False


def test_get_relative_action_left():
    assert get_relative_action(DIRECTION_RIGHT, DIRECTION_UP) == ACTION_LEFT
```

## Was macht diese Datei?

Diese Tests prüfen die Bewegung.

## TODOs

| TODO | Aufgabe                                  | Pflicht?    | Schwierigkeit |
| ---- | ---------------------------------------- | ----------- | ------------- |
| TL1  | Führe die Tests aus                     | ja          | leicht        |
| TL2  | Ergänze einen Test für die rechte Wand | ja          | mittel        |
| TL3  | Ergänze einen Test für die obere Wand  | Wahlaufgabe | mittel        |

## Datei: `tests/test_features.py`

```python
from engine.features import FEATURE_NAMES, extract_features


def test_extract_features_length():
    snake = [(5, 5), (4, 5), (3, 5)]
    direction = (1, 0)
    food = (10, 5)

    features = extract_features(snake, direction, food, 24, 18)

    assert len(features) == len(FEATURE_NAMES)


def test_food_right_feature():
    snake = [(5, 5), (4, 5), (3, 5)]
    direction = (1, 0)
    food = (10, 5)

    features = extract_features(snake, direction, food, 24, 18)

    food_right_index = FEATURE_NAMES.index("food_right")
    assert features[food_right_index] == 1


def test_danger_front_at_wall():
    snake = [(23, 5), (22, 5), (21, 5)]
    direction = (1, 0)
    food = (10, 5)

    features = extract_features(snake, direction, food, 24, 18)

    danger_front_index = FEATURE_NAMES.index("danger_front")
    assert features[danger_front_index] == 1
```

## Was macht diese Datei?

Diese Tests prüfen, ob der Spielzustand richtig in Zahlen umgewandelt wird.

## TODOs

| TODO | Aufgabe                                | Pflicht?    | Schwierigkeit |
| ---- | -------------------------------------- | ----------- | ------------- |
| TF1  | Führe die Tests aus                   | ja          | leicht        |
| TF2  | Ergänze einen Test für `food_left` | ja          | mittel        |
| TF3  | Ergänze einen Test für `food_up`   | Wahlaufgabe | mittel        |

## Datei: `tests/test_data_recorder.py`

```python
import csv

import pytest

from engine.data_recorder import CSV_HEADER, ensure_data_file, save_training_row


def test_ensure_data_file_creates_file(tmp_path):
    data_path = tmp_path / "training.csv"

    ensure_data_file(str(data_path))

    assert data_path.exists()


def test_ensure_data_file_writes_header(tmp_path):
    data_path = tmp_path / "training.csv"

    ensure_data_file(str(data_path))

    with open(data_path, "r", encoding="utf-8") as csv_file:
        reader = csv.reader(csv_file)
        header = next(reader)

    assert header == CSV_HEADER


def test_save_training_row(tmp_path):
    data_path = tmp_path / "training.csv"
    features = [0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1]
    action = 1

    save_training_row(features, action, str(data_path))

    with open(data_path, "r", encoding="utf-8") as csv_file:
        rows = list(csv.reader(csv_file))

    assert len(rows) == 2
    assert rows[1][-1] == "1"


def test_save_training_row_wrong_feature_count(tmp_path):
    data_path = tmp_path / "training.csv"
    features = [0, 1, 0]
    action = 1

    with pytest.raises(ValueError):
        save_training_row(features, action, str(data_path))
```

## Was macht diese Datei?

Diese Tests prüfen das Speichern der Trainingsdaten.

Diese Datei ist eher zum Ausführen als zum Ändern.

Pflicht: Tests ausführen
Wahlaufgabe: eigenen Test ergänzen

## Datei: `tests/test_ai_player.py`

```python
from engine.ai_player import load_model, predict_action
from engine.snake_logic import ACTION_STRAIGHT


class FakeModel:
    """
    Einfaches Testmodell.

    Es gibt immer die Aktion 2 zurück.
    """

    def predict(self, rows):
        return [2]


class BadFakeModel:
    """
    Fehlerhaftes Testmodell.

    Es gibt absichtlich eine ungültige Aktion zurück.
    """

    def predict(self, rows):
        return [99]


def test_load_model_missing_file(tmp_path):
    model_path = tmp_path / "missing_model.joblib"

    model = load_model(str(model_path))

    assert model is None


def test_predict_action_without_model():
    features = [0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1]

    action = predict_action(None, features)

    assert action == ACTION_STRAIGHT


def test_predict_action_with_fake_model():
    model = FakeModel()
    features = [0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1]

    action = predict_action(model, features)

    assert action == 2


def test_predict_action_invalid_model_output():
    model = BadFakeModel()
    features = [0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1]

    action = predict_action(model, features)

    assert action == ACTION_STRAIGHT
```

## Was macht diese Datei?

Diese Tests prüfen die KI-Schnittstelle.

Du brauchst dafür kein echtes Modell.

Das `FakeModel` ersetzt ein echtes Modell im Test.

Pflicht: Tests ausführen
Wahlaufgabe: eigenes FakeModel ergänzen

## Datei: `README.md`

```markdown
# SnakeTrainer

## Name

Name:

## Projektziel

Ich habe ein Snake-Spiel mit einem einfachen KI-Modus erstellt.

## Was habe ich geändert?

- Änderung 1:
- Änderung 2:
- Änderung 3:

## Was versteht die KI?

Die KI bekommt keine Bilder.

Sie bekommt Zahlen.

Diese Zahlen beschreiben die Spielsituation.

Beispiele:

- Gefahr vorne
- Gefahr links
- Futter links
- Futter rechts
- aktuelle Richtung

## Wie habe ich getestet?

Ich habe diesen Befehl ausgeführt:

```bash
pytest
```

Ergebnis:

```text
Hier füge ich meine Testausgabe ein.
```

## Modell trainieren

Ich habe diesen Befehl ausgeführt:

```bash
python train_model.py
```

Ergebnis:

```text
Hier füge ich die Ausgabe ein.
```

## Spiel testen

Ich habe das Spiel gestartet mit:

```bash
pgzrun game.py
```

## Score-Vergleich

| Versuch | Modus  | Score |
| ------: | ------ | ----: |
|       1 | Mensch |       |
|       2 | Mensch |       |
|       3 | Mensch |       |
|       4 | KI     |       |
|       5 | KI     |       |
|       6 | KI     |       |

## Reflexion

Was hat gut funktioniert?

Was war schwierig?

Was habe ich über KI gelernt?

Was würde ich mit mehr Zeit verbessern?

# 6. Schritt 3: Virtuelle Umgebung installieren

Jetzt richtest du Python ein.

Öffne das Terminal in VS Code.

## Windows

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

## macOS oder Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Prüfe die Installation

```bash
python --version
pip --version
```

Wenn keine Fehlermeldung kommt, ist das gut.

# 7. Schritt 4: Tests starten

Starte zuerst die Tests.

```bash
python -m pytest
```

oder kurz:

```bash
pytest
```

Du solltest sehen, dass Tests ausgeführt werden.

Wenn ein Test fehlschlägt, lies die Fehlermeldung ruhig durch.

Fehler sind normal.

Sie zeigen dir, wo du suchen musst.

## Pflichtabgabe

Du brauchst für die Abgabe:

```text
Screenshot oder Textausgabe von pytest
```

# 8. Schritt 5: Spiel starten

Starte das Spiel:

```bash
pgzrun game.py
```

## Bedienung

| Taste       | Wirkung               |
| ----------- | --------------------- |
| Pfeiltasten | Snake bewegen         |
| R           | Neustart              |
| K           | KI-Modus ein oder aus |

## Pflichtabgabe

Du brauchst für die Abgabe:

```text
Screenshot vom Spiel
```

# 9. Schritt 6: Sichtbare Änderungen machen

Öffne:

```text
student_config.py
```

Mache mindestens drei Änderungen.

Beispiele:

```text
Snake-Farbe ändern
Futter-Farbe ändern
Hintergrund ändern
Spielgeschwindigkeit ändern
Titel ändern
Game-Over-Text ändern
```

Starte danach das Spiel neu:

```bash
pgzrun game.py
```

## Pflichtabgabe

Du brauchst für die Abgabe:

```text
Liste deiner drei Änderungen
Screenshot vom angepassten Spiel
```

# 10. Schritt 7: Kleine Funktionen bearbeiten

Öffne:

```text
student_tasks.py
```

Bearbeite oder erkläre diese Funktionen:

```text
format_score()
format_high_score()
get_mode_text()
is_high_score()
```

## Pflicht

Du musst mindestens eine kleine Änderung machen.

Beispiel:

```python
return f"Punkte: {score}"
```

Dann Tests ausführen:

```bash
pytest
```

## Pflichtabgabe

Du brauchst:

```text
kurze Erklärung, welche Funktion du geändert hast
Testausgabe
```

# 11. Schritt 8: Features verstehen

Öffne:

```text
engine/features.py
```

Du musst diese Datei nicht komplett verstehen.

Aber du sollst drei Features erklären.

Beispiele:

| Feature             | Bedeutung                         |
| ------------------- | --------------------------------- |
| `danger_front`    | Vor der Snake ist Gefahr          |
| `food_left`       | Das Futter ist links vom Kopf     |
| `direction_right` | Die Snake bewegt sich nach rechts |

## Pflichtabgabe

Du brauchst in deiner README:

```text
Erklärung von 3 Features
```

# 12. Schritt 9: Trainingsdaten anschauen

Öffne:

```text
data/example_training.csv
```

Suche die letzte Spalte:

```text
action
```

Die Aktion bedeutet:

```text
0 = links
1 = geradeaus
2 = rechts
```

## Eigene Trainingsdaten

Wenn du das Spiel im Mensch-Modus spielst, werden eigene Daten gespeichert.

Die Datei heisst dann:

```text
data/snake_training.csv
```

## Pflichtabgabe

Du brauchst:

```text
Erklärung von einer CSV-Zeile in eigenen Worten
```

# 13. Schritt 10: Trainingsdaten erzeugen und Modell trainieren

Die KI braucht Trainingsdaten.

Wenn zu wenige Daten vorhanden sind, spielt die KI schlecht.
Sie fährt dann vielleicht direkt in die Wand oder immer im Kreis.

Darum erzeugst du zuerst automatisch Trainingsdaten.

## 10.1 Trainingsdaten erzeugen

Führe im Terminal aus:

```bash
python generate_training_data.py
```

Danach sollte diese Datei entstehen:

```text
data/snake_training.csv
```

Diese Datei enthält viele Beispiele für die KI.

Jede Zeile beschreibt eine Spielsituation:

```text
Gefahr vorne
Gefahr links
Gefahr rechts
Futterposition
aktuelle Richtung
gewählte Aktion
```

Die letzte Spalte heisst:

```text
action
```

Sie bedeutet:

```text
0 = links
1 = geradeaus
2 = rechts
```

Wenn alles funktioniert, siehst du ungefähr so eine Ausgabe:

```text
Trainingsdaten erzeugt
Anzahl Zeilen: 5120

Aktion 0 (links): ...
Aktion 1 (geradeaus): ...
Aktion 2 (rechts): ...

Gespeichert unter: data/snake_training.csv
```

## 10.2 Modell trainieren

Nach dem Erzeugen der Trainingsdaten musst du das Modell trainieren.

Führe aus:

```bash
python train_model.py
```

Danach sollte diese Datei entstehen:

```text
models/snake_mlp.joblib
```

Diese Datei ist das trainierte KI-Modell.

Das Spiel verwendet später genau dieses Modell im KI-Modus.

## Pflichtabgabe

Du brauchst:

```text
Screenshot oder Textausgabe von:
python generate_training_data.py
```

und:

```text
Nachweis, dass data/snake_training.csv existiert
```

Zusätzlich brauchst du:

```text
Screenshot oder Textausgabe von:
python train_model.py
```

und:

```text
Nachweis, dass models/snake_mlp.joblib existiert
```

## Was sollst du verstehen?

Du sollst diesen Ablauf erklären können:

```text
generate_training_data.py erstellt Beispiele.
train_model.py trainiert mit diesen Beispielen ein Modell.
game.py verwendet dieses Modell im KI-Modus.
```

Du musst nicht jede Zeile in `generate_training_data.py` verstehen.

Merke dir:

```text
Eine KI wird nur besser, wenn sie gute Beispiele bekommt.
```

# 14. Schritt 11: KI-Modus testen

Starte das Spiel:

```bash
pgzrun game.py
```

Drücke:

```text
K
```

Jetzt ist der KI-Modus aktiv.

Beobachte:

```text
Fährt die Snake geradeaus?
Weicht sie aus?
Findet sie Futter?
Stirbt sie schnell?
```

Die KI ist nicht perfekt.

Das ist normal.

Sie lernt nur aus den Daten.

## Pflichtabgabe

Du brauchst:

```text
kurze Beobachtung zum KI-Modus
```

# 15. Schritt 12: Score-Vergleich

Spiele mehrere Runden.

Fülle diese Tabelle aus.

| Versuch | Modus  | Score |
| ------: | ------ | ----: |
|       1 | Mensch |       |
|       2 | Mensch |       |
|       3 | Mensch |       |
|       4 | KI     |       |
|       5 | KI     |       |
|       6 | KI     |       |

## Fragen

Beantworte kurz:

```text
Wer war besser?
Warum war die KI gut oder schlecht?
Welche Daten hätte die KI noch gebraucht?
```

# 16. Übersicht der Pflichtaufgaben

| Nr. | Pflichtaufgabe                              | Datei / Ort                   |
| --: | ------------------------------------------- | ----------------------------- |
|   1 | Projektstruktur erstellen                   | gesamtes Projekt              |
|   2 | virtuelle Umgebung erstellen                | Terminal                      |
|   3 | Pakete installieren                         | `requirements.txt`          |
|   4 | Tests ausführen                            | `pytest`                    |
|   5 | Spiel starten                               | `pgzrun game.py`            |
|   6 | mindestens 3 sichtbare Änderungen          | `student_config.py`         |
|   7 | eine kleine Funktion ändern oder erklären | `student_tasks.py`          |
|   8 | 3 Features erklären                        | `engine/features.py`        |
|   9 | eine CSV-Zeile erklären                    | `data/example_training.csv` |
|  10 | Modell trainieren                           | `python train_model.py`     |
|  11 | KI-Modus testen                             | Taste K                       |
|  12 | Score-Vergleich ausfüllen                  | `README.md`                 |
|  13 | Reflexion schreiben                         | `README.md`                 |

# 17. Wahlaufgaben

Wenn du früher fertig bist, wähle eine Aufgabe.

| Wahlaufgabe | Beschreibung                     | Schwierigkeit |
| ----------- | -------------------------------- | ------------- |
| W1          | eigenes Farbschema erstellen     | leicht        |
| W2          | Game-Over-Text schöner machen   | leicht        |
| W3          | mehr Trainingsdaten sammeln      | mittel        |
| W4          | `hidden_layer_sizes`verändern | mittel        |
| W5          | zusätzlichen Test schreiben     | mittel        |
| W6          | KI-Status schöner anzeigen      | mittel        |
| W7          | neues Feature ergänzen          | anspruchsvoll |
| W8          | Hindernisse einbauen             | anspruchsvoll |

# 18. Was du nicht machen musst

Du musst nicht:

```text
ein neuronales Netz selbst programmieren
Backpropagation erklären
alle scikit-learn-Zeilen verstehen
den ganzen Code auswendig kennen
ein perfektes Spiel bauen
eine perfekte KI bauen
```

Das Ziel ist:

```text
Du kannst ein vorbereitetes Projekt starten.
Du kannst kleine Änderungen machen.
Du kannst Tests ausführen.
Du kannst erklären, wie die KI grob verwendet wird.
```

# 19. Häufige Probleme

## Problem: `pgzrun` wird nicht gefunden

Prüfe zuerst:

```bash
pip install -r requirements.txt
```

Prüfe auch, ob die virtuelle Umgebung aktiv ist.

## Problem: Das Modell fehlt

Trainiere zuerst:

```bash
python train_model.py
```

## Problem: Die KI spielt schlecht

Das ist normal.

Mögliche Gründe:

```text
zu wenige Trainingsdaten
schlechte Trainingsdaten
Features reichen nicht
Modell ist sehr einfach
```

## Problem: Tests schlagen fehl

Lies die Fehlermeldung.

Meist steht dort:

```text
welche Datei betroffen ist
welcher Test betroffen ist
was erwartet wurde
was wirklich zurückkam
```

Das hilft dir.

# 20. Abgabe

Gib am Schluss ab:

```text
1. dein vollständiges Projekt
2. deine README.md
3. Screenshot vom Spiel
4. Screenshot oder Textausgabe von pytest
5. Screenshot oder Textausgabe vom Modelltraining
6. deine Score-Tabelle
7. kurze Reflexion
```

# 21. Bewertung

## Produkt: 50 %

| Kriterium                            | Punkte |
| ------------------------------------ | -----: |
| Projekt startet korrekt              |      8 |
| Spiel läuft stabil                  |      8 |
| sichtbare Änderungen sind vorhanden |     10 |
| KI-Modus wurde getestet              |      8 |
| Modell wurde trainiert               |      8 |
| Tests wurden ausgeführt             |      8 |

## Dokumentation: 30 %

| Kriterium                               | Punkte |
| --------------------------------------- | -----: |
| README ist ausgefüllt                  |      6 |
| Änderungen sind beschrieben            |      6 |
| 3 Features sind erklärt                |      6 |
| CSV-Zeile ist erklärt                  |      4 |
| Score-Vergleich ist ausgefüllt         |      4 |
| Reflexion ist ehrlich und verständlich |      4 |

## Arbeitsprozess: 20 %

| Kriterium                       | Punkte |
| ------------------------------- | -----: |
| du hast regelmässig gearbeitet |      5 |
| du hast Probleme beschrieben    |      5 |
| du hast Tests genutzt           |      5 |
| du hast dein Projekt verbessert |      5 |

# 22. Merksatz

```text
student_config.py verändert das Aussehen.
student_tasks.py enthält kleine Aufgaben.
game.py zeigt das Spiel.
snake_logic.py berechnet Regeln.
features.py macht Zahlen für die KI.
data_recorder.py sammelt Beispiele.
train_model.py trainiert das Modell.
ai_player.py benutzt das Modell.
tests prüfen deinen Code.
```

Du musst nicht alles perfekt verstehen.

Aber du sollst zeigen:

```text
Ich kann ein Projekt starten.
Ich kann Code gezielt ändern.
Ich kann Tests ausführen.
Ich kann eine einfache KI im Spiel verwenden.
```
