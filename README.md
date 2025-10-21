#  DocuLingo

**DocuLingo**, yapay zekâ destekli, iki dilli (Türkçe – İngilizce) belge özetleme ve soru-cevap uygulamasıdır.  
Kullanıcılar, yükledikleri **Türkçe veya İngilizce PDF dosyalarını** Türkçe->İngilizce veya İngilizce->Türkçe'ye çevirerek özetini çıkarabilir ve içerikle ilgili sorular sorabilirler.  
Uygulama, **RAG (Retrieval-Augmented Generation)** mimarisiyle çalışır ve metinleri anlamlı parçalara bölüp vektör veritabanında depolayarak **bağlama dayalı yanıtlar** üretir.

DocuLingo, uzun akademik veya teknik metinleri hızlıca anlamak isteyen öğrenciler, araştırmacılar ve profesyoneller için geliştirilmiştir.  
Kullanıcı, özetin **Türkçe mi İngilizce mi** olacağını seçebilir ve ardından belgeyle sohbet edebilir.

---

##  DocuLingo RAG Mimarisi

Uygulama eksiksiz bir **Retrieval-Augmented Generation** sürecini izler:

1. **İçerik Çıkarma:** PDF dosyalarından metinler *PyPDF2* ile alınır.  
2. **Metin Bölme:** Belge boyutuna göre dinamik olarak anlamlı parçalara ayrılır.  
3. **Vektörleştirme:** Metin parçaları, **HuggingFace Sentence Transformers (all-MiniLM-L6-v2)** modeliyle vektörlere dönüştürülür.  
4. **Vektör Depolama:** Vektörler **Chroma** veritabanında saklanır.  
5. **Bağlam Eşleme:** *LangChain ConversationalRetrievalChain* ile en alakalı bölümler bulunur.  
6. **Yanıt Üretimi:** **Google Gemini 2.0 Flash** modeliyle özet ve cevap oluşturulur.

---

##  Desteklenen Diller
-  **Belge dili:** Türkçe 🇹🇷 veya İngilizce 🇬🇧  
-  **Özet dili:** Kullanıcı seçimine göre Türkçe veya İngilizce  
-  **Soru-cevap:** Her iki dili de anlayabilir

---

##  Özellikler ve Kullanım Alanları

-  **Akıllı Özetleme:** Yüklenen PDF’lerin kısa ve odaklı özetlerini üretir.  
-  **Dil Seçimi:** Özetin Türkçe veya İngilizce hazırlanmasını sağlar.  
-  **Sohbet Tabanlı Q&A:** Belgeyle ilgili doğal dilde sorulara yanıt verir.  
-  **Bağlama Dayalı Yanıtlar:** Yanıtlar sadece belge içeriğine dayanır.  
-  **Dinamik İşleme:** PDF boyutuna göre parça uzunluğunu otomatik ayarlar.  
-  **Kullanım Alanları:**
  - Akademik makale özetleme  
  - Teknik rapor inceleme  
  - Öğrenciler ve araştırmacılar için hızlı içerik analizi  

---

## Veri Seti Açıklaması
- Bu proje hazır bir veri seti yerine, kullanıcı tarafından yüklenen PDF belgelerini dinamik olarak işlemektedir.
Kullanıcı, sistem üzerinden İngilizce veya Türkçe içerikli bir PDF yükler. Bu dosya, model tarafından metne dönüştürülür, özetlenir ve vektör veritabanına aktarılır.
Bu yaklaşım, proje kapsamında “dinamik veri üretimi” olarak değerlendirilmiştir.

- Proje geliştirilirken “Paper-Bold” adlı açık kaynak projesinden teknik mimari açısından ilham alınmıştır, ancak tüm kodlar DocuLingo için yeniden uyarlanmış ve özelleştirilmiştir.
Herhangi bir hazır veri seti doğrudan kullanılmamıştır.

---


##  Kullanılan Teknolojiler

- **Backend:** Python  
- **Arayüz:** Gradio (Colab uyumlu) (https://0834cedf069ce7914d.gradio.live)
- **Yapay Zekâ:** Google Gemini 2.0 Flash, LangChain  
- **Embedding:** HuggingFace Sentence Transformers  
- **Vektör Veritabanı:** Chroma  
- **PDF İşleme:** PyPDF2  

---
##  Kurulum ve Çalıştırma

1. Not defterini Colab'da aç
   ```bash
   DocuLingo.ipynb dosyasını Google Colab’da açın (File → Open with Colab).
   ```

2. Gerekli paketleri kur
   (Aşağıdaki hücreyi çalıştırın):
   ```bash
   pip install -q gradio google-generativeai PyPDF2 langchain langchain-community langchain-chroma sentence-transformers
   ```

3. API anahtarını güvenli alın
   ```bash
   import os, getpass
   GOOGLE_API_KEY = os.getenv("GOOGLE_API_KEY") or getpass.getpass("🔑 Gemini API Key: ")

   ```

4. Uygulamayı başlat
   ```
   Not defterindeki ilgili hücreleri sırayla çalıştırın.
   Gradio arayüz bağlantısı çıktı olarak görünecektir (Running on public URL: https://14a15b37b26c95a33e.gradio.live)
   ```
