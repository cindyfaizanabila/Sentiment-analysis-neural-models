<<<<<<< HEAD
# Twitter Entity Sentiment: ANN vs RNN vs LSTM vs GRU vs BiLSTM

Perbandingan lima arsitektur neural network (TensorFlow/Keras) untuk klasifikasi sentimen tweet berbahasa Inggris (Negative / Neutral / Positive) pada dataset *Twitter Entity Sentiment Analysis*.

> Tugas Praktikum Pertemuan 7 - Pembelajaran Mesin / Deep Learning

## Ringkasan

| Item | Detail |
|---|---|
| Dataset | Twitter Entity Sentiment Analysis (Kaggle), `training.csv`, 74.682 baris |
| Label dipakai | Negative, Neutral, Positive (kelas `Irrelevant` dibuang) |
| Data setelah cleaning | 54.942 tweet (dedup berdasarkan teks + label) |
| Split | 70% train / 10% val / 20% test, **GroupShuffleSplit by tweet `id`** (tidak ada kebocoran antar split) |
| Preprocessing | lowercase, hapus URL/mention/entitas HTML/angka/tanda baca |
| Representasi | `TextVectorization` (vocab 20.000, panjang 48 token = persentil 95) + Embedding 100 dim (dilatih dari nol) |
| Model | ANN (GlobalAvgPool + Dense), SimpleRNN, LSTM, GRU, BiLSTM |
| Variasi | V1 (64 unit, dropout 0.3) dan V2 (128 unit, dropout 0.5) |

## Hasil pada Data Test

| Model | Accuracy | Precision | Recall | F1 (weighted) | F1 (macro) |
|---|---|---|---|---|---|
| **ANN-V1** | **0.6276** | **0.6276** | **0.6276** | **0.6262** | **0.6211** |
| LSTM-V1 | 0.6170 | 0.6156 | 0.6170 | 0.6145 | 0.6087 |
| BiLSTM-V1 | 0.6004 | 0.5994 | 0.6004 | 0.5987 | 0.5925 |
| GRU-V1 | 0.5972 | 0.5955 | 0.5972 | 0.5938 | 0.5870 |
| RNN-V2 | 0.5986 | 0.6001 | 0.5986 | 0.5911 | 0.5836 |

## Temuan dan Keterbatasan

- **Model sederhana (ANN) mengalahkan semua model sekuensial.** Artinya, dengan setup ini (embedding dari nol, data ~38 ribu), urutan kata belum memberi keuntungan nyata dibanding rata-rata embedding.
- **Overfitting kuat.** Akurasi train mencapai 89-97% pada epoch 2-3, sementara akurasi validasi turun dari epoch 1. Dengan `EarlyStopping(restore_best_weights=True)`, bobot terbaik praktis berasal dari **epoch 1**.
- **Hyperparameter tuning terbatas:** hanya dua variasi (units dan dropout berubah bersamaan), sehingga pengaruh tiap parameter tidak bisa dipisahkan.
- Kelas `Neutral` paling sulit diprediksi (F1 ~0.54 pada ANN-V1).
- Akurasi ~63% masih rendah; hasil ini adalah baseline, bukan model siap pakai.

## Ide Pengembangan

- Embedding pra-latih (GloVe / fastText) atau fine-tuning model Transformer (mis. DistilBERT, IndoBERT bila data Indonesia).
- Regularisasi lebih kuat: dropout pada embedding, `recurrent_dropout`, L2, dan learning rate lebih kecil.
- Tuning terpisah (grid/random search atau Keras Tuner) untuk units, dropout, dan learning rate.
- Pertimbangkan class weight / augmentasi untuk kelas Neutral.

## Cara Menjalankan

```bash
git clone https://github.com/<username>/twitter-entity-sentiment-neural-networks.git
cd twitter-entity-sentiment-neural-networks
pip install -r requirements.txt
```

1. Unduh `twitter_training.csv` dari Kaggle: *Twitter Entity Sentiment Analysis* (jhana / jp797498e).
2. Simpan sebagai `training.csv` di folder `data/` (atau upload saat diminta di Colab).
3. Buka `sentiment-analysis-neural-models.ipynb` di Google Colab atau Jupyter, lalu *Run all*.

> Dataset tidak disertakan di repo ini; ikuti lisensi dari sumber aslinya.

## Struktur Repo

```
.
├── sentiment-analysis-neural-models.ipynb
├── README.md
├── requirements.txt
├── .gitignore
└── data/            # (diabaikan git) taruh training.csv di sini
```

## Tech Stack

Python, TensorFlow/Keras, scikit-learn, pandas, NumPy, Matplotlib, Seaborn.

## Penulis

Cindy Faiza Nabila - Teknik Informatika, Universitas Negeri Malang
=======
# Sentiment-analysis-neural-models
Comparing ANN, RNN, LSTM, GRU, and BiLSTM for 3-class tweet sentiment classification with leakage-free group splits
>>>>>>> 735fcb8b970a88d941dac46a7e9bc082b6159e64
