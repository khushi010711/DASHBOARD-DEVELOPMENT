# DASHBOARD-DEVELOPMENT

import dash
from dash import dcc, html, Input, Output
import pandas as pd
import numpy as np
import plotly.express as px

# Simulate financial transaction dataset
np.random.seed(42)
n_rows = 100_000
categories = ['Groceries', 'Electronics', 'Clothing', 'Entertainment', 'Health']
customers = ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve']

df = pd.DataFrame({
    'transaction_id': np.arange(n_rows),
    'category': np.random.choice(categories, n_rows),
    'customer': np.random.choice(customers, n_rows),
    'amount': np.random.uniform(5, 500, n_rows)  # transaction amounts between $5 and $500
})

# Start Dash app
app = dash.Dash(__name__)
app.title = "Financial Transactions Dashboard"

# Layout
app.layout = html.Div([
    html.H1("Interactive Financial Transactions Dashboard"),

    dcc.Dropdown(
        id='customer-dropdown',
        options=[{'label': cust, 'value': cust} for cust in df['customer'].unique()],
        value='Alice',
        clearable=False
    ),

    html.Div([
        dcc.Graph(id='total-transactions-category'),
        dcc.Graph(id='avg-transaction-customer'),
    ], style={'display': 'flex', 'gap': '2rem'}),

    dcc.Graph(id='transaction-amount-distribution')
])

# Callbacks
@app.callback(
    Output('total-transactions-category', 'figure'),
    Output('avg-transaction-customer', 'figure'),
    Output('transaction-amount-distribution', 'figure'),
    Input('customer-dropdown', 'value')
)
def update_dashboard(selected_customer):
    # Total transactions by category
    transactions_by_category = df.groupby('category')['amount'].sum().reset_index()
    fig1 = px.bar(transactions_by_category, x='category', y='amount', title='Total Transactions by Category')

    # Average transaction by customer
    customer_avg = df[df['customer'] == selected_customer].groupby('category')['amount'].mean().reset_index()
    fig2 = px.bar(customer_avg, x='category', y='amount', title=f'Avg Transaction Value - {selected_customer}')

    # Distribution of transaction amounts
    fig3 = px.histogram(df, x='amount', nbins=50, title='Transaction Amount Distribution')

    return fig1, fig2, fig3

# Run the app
if __name__ == '__main__':
    app.run(debug=True)


