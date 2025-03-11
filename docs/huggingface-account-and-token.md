# HuggingFace Account Setup and Token Guide

## Create Account
1. Go to https://huggingface.co/
2. Click "Sign Up" (top-right)
3. Register with email, Google, or GitHub
4. Verify your email

## Get Access Token
1. Click your profile picture → "Settings"
2. Select "Access Tokens" in sidebar
3. Click "New Token"
4. Name your token (e.g., "Python Projects")
5. Select "Write" permission
6. Set expiration date (or "No expiration")
7. Click "Generate Token"
8. Copy and save your token securely

## Use Token in Python
```python
import os
from huggingface_hub import HfApi

# Set token as environment variable
os.environ["HUGGINGFACE_TOKEN"] = "your_token_here"

# Or use directly
api = HfApi(token="your_token_here")

# Test token
my_models = api.list_models(author="your-username")
print(my_models)
```

## Use Token in Kaggle
1. Install required libraries:
   ```python
   !pip install -q huggingface_hub transformers
   ```

2. Store token in Kaggle secrets:
   - Go to account settings → "Secrets"
   - Add new secret named `HUGGINGFACE_TOKEN`
   - Paste your token as the value

3. Access token in notebook:
   ```python
   import os
   from kaggle_secrets import UserSecretsClient
   
   # Get token from Kaggle secrets
   user_secrets = UserSecretsClient()
   os.environ["HUGGINGFACE_TOKEN"] = user_secrets.get_secret("HUGGINGFACE_TOKEN")
   
   # Use the HuggingFace API
   from huggingface_hub import HfApi
   api = HfApi()
   ```

## Use Token in Google Colab
1. Install required libraries:
   ```python
   !pip install -q huggingface_hub transformers
   ```

2. Use Google Colab's Secrets:
   - Click on the key icon in the left sidebar
   - Add a new secret with name `HUGGINGFACE_TOKEN` and your token as value

3. Access the token in your notebook:
   ```python
   import os
   from google.colab import userdata
   
   # Get token from Colab secrets
   os.environ["HUGGINGFACE_TOKEN"] = userdata.get('HUGGINGFACE_TOKEN')
   
   # Use the HuggingFace API
   from huggingface_hub import HfApi
   api = HfApi()
   
   # Example: Upload a file
   api.upload_file(
       path_or_fileobj="./model.h5",
       path_in_repo="model.h5",
       repo_id="your-username/your-model",
       repo_type="model"
   )
   ```

4. Alternative method (temporary, less secure):
   ```python
   # Only use for testing, not for shared notebooks
   import os
   os.environ["HUGGINGFACE_TOKEN"] = "your_token_here"
   ```

## Security Tips
- Never share your token publicly
- Don't commit token to version control
- Use environment variables when possible
- Revoke compromised tokens immediately