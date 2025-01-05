1. Add API Key vào openAI => Models tự động được tạo 
2. Với Ollama, 
- thì có sẵn ollama 2 sau khi kích hoạt hoặc chạy ollama dưới nền thì phải 
- Lúc đó đang chạy docker nên là bạn click vào : http://host.docker.internal:11434 để add thêm model từ huggingface nhé 

---
Dưới đây là lệnh **1 dòng** để chạy mỗi container trong terminal:

### **Chạy Pipelines**
```bash
docker run -d -p 9099:9099 --add-host=host.docker.internal:host-gateway -v pipelines:/app/pipelines -e PIPELINES_URLS="https://raw.githubusercontent.com/open-webui/pipelines/main/examples/pipelines/rag/haystack_pipeline.py" --name pipelines --restart always ghcr.io/open-webui/pipelines:main
```

---

### **Chạy Open WebUI**
```bash
docker run -d -p 3000:8080 -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

Cách set up này đủ để chạy openAI, ollama, còn pipeline thì đang bug. 

---

3. Với việc add pipeline thì: 

Run container: 
```
docker run -d -p 9099:9099 --add-host=host.docker.internal:host-gateway -v pipelines:/app/pipelines --name pipelines --restart always ghcr.io/open-webui/pipelines:main
```

Sử dụng pipeline example có sẵn: 
```
docker run -d -p 9099:9099 --add-host=host.docker.internal:host-gateway -v pipelines:/app/pipelines -e PIPELINES_URLS="https://raw.githubusercontent.com/open-webui/pipelines/blob/main/examples/pipelines/rag/haystack_pipeline.py" --name pipelines --restart always ghcr.io/open-webui/pipelines:main
```



Add : 
```
- Set the API URL to http://localhost:9099 (Docker: `http://host.docker.internal:9099`) and the API key to `0p3n-w3bu!`.

crul: 
```
curl --location 'http://host.docker.internal:9099/api/tags'
```