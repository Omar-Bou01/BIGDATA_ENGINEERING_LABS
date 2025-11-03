# 🎓 Ingénierie Big Data - Labs Hadoop & MapReduce

> Exercices pratiques explorant le calcul distribué avec Hadoop HDFS et MapReduce

[![Hadoop](https://img.shields.io/badge/Hadoop-3.2.0-yellow?logo=apache-hadoop)](https://hadoop.apache.org/)
[![Java](https://img.shields.io/badge/Java-8-red?logo=java)](https://www.java.com/)
[![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)](https://www.python.org/)

---

## 🎯 Aperçu

Ce dépôt contient des travaux pratiques Hadoop couvrant le stockage de fichiers distribués (HDFS) et le traitement parallèle avec MapReduce. Les exercices progressent des opérations de fichiers de base aux pipelines complets de traitement de données en Java et Python.

---

## 📂 Structure du Projet

```
BIGDATA_ENGINEERING_LABS/
│
├── hadoop_lab0_lab2/              # Opérations HDFS
│   ├── HadoopFileStatus.java     # Récupération métadonnées
│   ├── ReadHDFS.java              # Lecture depuis HDFS
│   ├── HDFSWrite.java             # Écriture vers HDFS
│   └── pom.xml
│
├── lab3_mapreduce/                # Implémentation MapReduce
│   ├── WordCount.java             # WordCount en Java
│   ├── pom.xml
│   └── reponses_commandes_lab3.sh
│
└── datasets/
    ├── mapper.py                  # Mapper Python
    └── reducer.py                 # Reducer Python
```

---

## 📚 Description des Labs

### 🔷 Labs 0–2 : Opérations sur Fichiers HDFS

Interactions basiques avec HDFS utilisant des programmes Java pour comprendre le stockage de fichiers distribués.

**Programmes Clés :**

```bash
# Obtenir les métadonnées d'un fichier
hadoop jar hadoop_lab-1.0-SNAPSHOT-HadoopFileStatus.jar /user/root/input purchases.txt

# Lire un fichier depuis HDFS
hadoop jar hadoop_lab-1.0-SNAPSHOT-ReadHDFS.jar /user/root/input/achats.txt

# Écrire dans HDFS
hadoop jar hadoop_lab-1.0-SNAPSHOT-HDFSWrite.jar /input/bonjour.txt "Bonjour HDFS"
```

---

### 🔶 Lab 3 : MapReduce WordCount

Implémentation du WordCount avec deux approches différentes :

#### **Java MapReduce :**
```bash
# Nettoyage et exécution
hdfs dfs -rm -r /user/root/output
hadoop jar WordCount.jar /user/root/input/achats.txt /user/root/output

# Afficher les résultats
hdfs dfs -cat /user/root/output/part-r-00000 | head -20
```

#### **Python Streaming :**
```bash
# Exécuter le job streaming
hadoop jar $HADOOP_HOME/share/hadoop/tools/lib/hadoop-streaming-3.2.0.jar \
    -files mapper.py,reducer.py \
    -mapper "python3 mapper.py" \
    -reducer "python3 reducer.py" \
    -input /user/root/input/achats.txt \
    -output /user/root/output_py

# Afficher les résultats
hdfs dfs -cat /user/root/output_py/part-00000 | tail -20
```

---

## 🔍 Comparaison : Java vs Python Streaming

| **Critère** | **Java MapReduce** | **Python Streaming** |
|-------------|-------------------|---------------------|
| **Performance** | ⚡ Rapide - JVM natif | 🐢 Plus lent - Surcharge processus |
| **Développement** | 🐌 Complexe - Compilation requise | ⚡ Simple - Script et exécution |
| **Meilleur Pour** | Production, gros volumes | Prototypage, analyse rapide |
| **Sécurité Type** | ✅ Vérification à la compilation | ⚠️ Erreurs uniquement à l'exécution |

**Conclusion :** Java pour la production, Python pour le développement rapide et l'exploration.

---

## 🚀 Démarrage Rapide

```bash
# 1. Démarrer Hadoop
start-dfs.sh && start-yarn.sh

# 2. Télécharger les données
hdfs dfs -mkdir -p /user/root/input
hdfs dfs -put achats.txt /user/root/input/

# 3. Exécuter votre job MapReduce
hadoop jar WordCount.jar /user/root/input/achats.txt /user/root/output

# 4. Vérifier les résultats
hdfs dfs -cat /user/root/output/part-r-00000
```

---

## 🎓 Acquis d'Apprentissage

À travers ces labs, j'ai acquis :
- ✅ Expérience pratique avec les opérations de cluster Hadoop
- ✅ Compréhension des systèmes de fichiers distribués et de la localité des données
- ✅ Programmation MapReduce en Java et Python
- ✅ Analyse de performance de différentes approches d'implémentation
- ✅ Débogage d'applications distribuées

---

## 🛠️ Technologies Utilisées

- **Hadoop** 3.2.0 - Framework de calcul distribué
- **Java** 8 - Jobs MapReduce compilés
- **Python** 3.x - Scripts MapReduce streaming
- **Maven** - Automatisation de build
- **Docker** - Déploiement de cluster conteneurisé

---

## 👨‍💻 Auteur

**Omar BOUZIANE**  
_Étudiant Ingénieur en Data Science & Business Intelligence_
