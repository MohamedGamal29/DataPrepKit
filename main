import pandas as pd

class DataPrep:
    # Data Reading
    @staticmethod
    def read_file(file_format, file_path):
        supported_formats = ['csv', 'excel', 'json']
        if file_format not in supported_formats:
            raise ValueError("Unsupported file format")
        
        try:
            if file_format == 'csv':
                data = pd.read_csv(file_path)
            elif file_format == 'excel':
                data = pd.read_excel(file_path)
            elif file_format == 'json':
                data = pd.read_json(file_path)
        except Exception as e:
            raise RuntimeError(f"Error reading file: {e}")
            
        return data
    
    # Handling Missing Values 
    @staticmethod
    def missing_values(data, strategy='remove'):
        supported_strategies = ['remove', 'mode', 'mean', 'median']
        if strategy not in supported_strategies:
            raise ValueError("Unsupported missing values strategy")

        if strategy == 'remove':
            return data.dropna()
        else:
            # Handle missing values based on strategy
            for col in data.columns:
                if data[col].dtype == 'O' or strategy == 'mode':
                    data[col] = data[col].fillna(data[col].mode().iloc[0])
                elif strategy == 'mean':
                    data[col] = data[col].fillna(data[col].mean())
                elif strategy == 'median':
                    data[col] = data[col].fillna(data[col].median())
            return data
    
    # Data Summary
    @staticmethod
    def data_summary(data):
        for col in data.columns:
            print(f"{col} column summary")
            if data[col].dtype != 'O':
                print(f"The maximum value is: {data[col].max()}")
                print(f"The minimum value is: {data[col].min()}")
                print(f"The mean of the column is: {data[col].mean()}")
                print(f"The median of the column is: {data[col].median()}")
                print(f"The mode of the column is: {data[col].mode().iloc[0]}")
            else:
                print(f"The mode of the column is: {data[col].mode().iloc[0]}")

    # Data Encoding
    @staticmethod
    def encode(data, column):
        categories = data[column].unique()
        mapping = {category: i for i, category in enumerate(categories)}
        encoded_data = data.copy()
        encoded_data[column] = encoded_data[column].map(mapping)
        return categories, encoded_data
    
    # Data Decoding
    @staticmethod
    def decode(data, column, categories):
        decoded_data = data.copy()
        decoded_data[column] = decoded_data[column].map({i: category for i, category in enumerate(categories)})
        return decoded_data
