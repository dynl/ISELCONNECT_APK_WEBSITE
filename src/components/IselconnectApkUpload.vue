<template>
  <div class="upload-wrapper">
    <h2>Upload ISELCONNECT APK</h2>
    
    <div 
      class="upload-area" 
      @dragover.prevent 
      @drop.prevent="handleDrop"
      @click="triggerFileInput"
    >
      <input 
        type="file" 
        ref="fileInput" 
        accept=".apk, application/vnd.android.package-archive" 
        @change="handleFileSelect" 
        class="hidden-input"
      />
      
      <div v-if="!selectedFile" class="upload-placeholder">
        <svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"></path>
          <polyline points="17 8 12 3 7 8"></polyline>
          <line x1="12" y1="3" x2="12" y2="15"></line>
        </svg>
        <p>Click or drag your <strong>ISELCONNECT .apk</strong> file here</p>
      </div>

      <div v-else class="file-details">
        <p class="file-name">📄 {{ selectedFile.name }}</p>
        <p class="file-size">{{ formatFileSize(selectedFile.size) }}</p>
        <button @click.stop="removeFile" class="remove-btn">Remove File</button>
      </div>
    </div>

    <button 
      :disabled="!selectedFile || isUploading" 
      @click="uploadApk" 
      class="upload-btn"
    >
      {{ isUploading ? 'Uploading...' : 'Upload Application' }}
    </button>
    
    <p v-if="uploadStatus" :class="['status-message', uploadStatus.type]">
      {{ uploadStatus.text }}
    </p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const fileInput = ref(null);
const selectedFile = ref(null);
const isUploading = ref(false);
const uploadStatus = ref(null);

// Trigger the hidden HTML file input when the styled area is clicked
const triggerFileInput = () => {
  if (fileInput.value) {
    fileInput.value.click();
  }
};

// Validate if the dropped/selected file is an Android APK
const isValidApk = (file) => {
  return file.name.endsWith('.apk') || file.type === 'application/vnd.android.package-archive';
};

// Handle standard file input selection
const handleFileSelect = (event) => {
  const file = event.target.files[0];
  processFile(file);
};

// Handle drag and drop selection
const handleDrop = (event) => {
  const file = event.dataTransfer.files[0];
  processFile(file);
};

// Process and validate the selected file
const processFile = (file) => {
  uploadStatus.value = null;
  
  if (!file) return;

  if (!isValidApk(file)) {
    uploadStatus.value = { 
      type: 'error', 
      text: 'Invalid file type. Please upload a valid .apk file.' 
    };
    selectedFile.value = null;
    return;
  }

  selectedFile.value = file;
};

// Clear the current selection
const removeFile = () => {
  selectedFile.value = null;
  uploadStatus.value = null;
  if (fileInput.value) {
    fileInput.value.value = ''; // Reset actual input
  }
};

// Convert raw bytes into readable sizes
const formatFileSize = (bytes) => {
  if (bytes === 0) return '0 Bytes';
  const k = 1024;
  const sizes = ['Bytes', 'KB', 'MB', 'GB'];
  const i = Math.floor(Math.log(bytes) / Math.log(k));
  return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
};

// Handle submission to your backend API
const uploadApk = async () => {
  if (!selectedFile.value) return;

  isUploading.value = true;
  uploadStatus.value = null;

  // Package the file securely for multipart/form-data upload
  const formData = new FormData();
  formData.append('apkFile', selectedFile.value);
  formData.append('appName', 'ISELCONNECT');

  try {
    // TODO: Replace this URL with your actual backend endpoint
    /*
    const response = await fetch('/api/upload-apk', {
      method: 'POST',
      body: formData
    });
    
    if (!response.ok) throw new Error('Upload failed');
    */

    // Simulating an API call for demonstration
    await new Promise(resolve => setTimeout(resolve, 2000));

    uploadStatus.value = { 
      type: 'success', 
      text: 'ISELCONNECT APK uploaded successfully!' 
    };
    
    // Clear form on success
    setTimeout(() => {
      removeFile();
    }, 2000);

  } catch (error) {
    uploadStatus.value = { 
      type: 'error', 
      text: 'Upload failed. Please check your network and try again.' 
    };
  } finally {
    isUploading.value = false;
  }
};
</script>

<style scoped>
.upload-wrapper {
  max-width: 500px;
  margin: 0 auto;
  font-family: Arial, sans-serif;
}

.upload-wrapper h2 {
  text-align: center;
  color: #333;
}

.upload-area {
  border: 2px dashed #cbd5e1;
  border-radius: 8px;
  padding: 40px 20px;
  text-align: center;
  cursor: pointer;
  background-color: #f8fafc;
  transition: all 0.3s ease;
}

.upload-area:hover {
  border-color: #3b82f6;
  background-color: #eff6ff;
}

.hidden-input {
  display: none;
}

.upload-placeholder {
  color: #64748b;
}

.upload-placeholder svg {
  margin-bottom: 12px;
  color: #94a3b8;
}

.file-details {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
}

.file-name {
  font-weight: bold;
  color: #1e293b;
  margin: 0;
}

.file-size {
  color: #64748b;
  font-size: 0.9em;
  margin: 0;
}

.remove-btn {
  background: none;
  border: none;
  color: #ef4444;
  cursor: pointer;
  text-decoration: underline;
  padding: 4px 8px;
  margin-top: 8px;
}

.upload-btn {
  width: 100%;
  padding: 12px;
  background-color: #3b82f6;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 16px;
  font-weight: bold;
  margin-top: 16px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.upload-btn:disabled {
  background-color: #94a3b8;
  cursor: not-allowed;
}

.upload-btn:not(:disabled):hover {
  background-color: #2563eb;
}

.status-message {
  margin-top: 16px;
  padding: 12px;
  border-radius: 6px;
  text-align: center;
  font-weight: 500;
}

.status-message.success {
  background-color: #dcfce7;
  color: #166534;
  border: 1px solid #bbf7d0;
}

.status-message.error {
  background-color: #fee2e2;
  color: #991b1b;
  border: 1px solid #fecaca;
}
</style>