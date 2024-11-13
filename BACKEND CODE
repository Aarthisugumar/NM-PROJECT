const express = require('express');
const mongoose = require('mongoose');
const bodyParser = require('body-parser');
const cors = require('cors');

const app = express();
const PORT = 5000;

app.use(bodyParser.json());
app.use(cors());

mongoose.connect('mongodb://localhost:27017/bookstore', {
    useNewUrlParser: true,
    useUnifiedTopology: true,
}).then(() => console.log('Connected to MongoDB')).catch(err => console.error('Connection error:', err));

const bookSchema = new mongoose.Schema({
    title: String,
    author: String,
});
const Book = mongoose.model('Book', bookSchema);

app.get('/api/books', async (req, res) => {
    try {
        const books = await Book.find();
        res.json(books);
    } catch (err) {
        res.status(500).json({ message: 'Error fetching books' });
    }
});

app.post('/api/payment', (req, res) => {
    const paymentData = req.body;
    if (paymentData) {
        res.status(200).json({ message: 'Payment processed successfully', status: 'success' });
    } else {
        res.status(400).json({ message: 'Invalid payment data', status: 'failure' });
    }
});

app.post('/api/confirm-order', (req, res) => {
    const orderData = req.body;
    if (orderData) {
        res.status(200).json({ message: 'Order confirmed', orderDetails: orderData });
    } else {
        res.status(400).json({ message: 'Order confirmation failed' });
    }
});

app.listen(PORT, () => {
    console.log(`Server running on http://localhost:${PORT}`);
});
