# sign-up-form
management
import React, { useState } from 'react';

const SignupForm = () => {
  const [username, setUsername] = useState('');
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [errors, setErrors] = useState({
    username: '',
    email: '',
    password: '',
  });
  const [isSubmitted, setIsSubmitted] = useState(false);
  const [formData, setFormData] = useState('');

  const validateForm = () => {
    const newErrors = {
      username: '',
      email: '',
      password: '',
    };

    if (username.length < 3) {
      newErrors.username = 'Username should be at least 3 characters';
    }

    if (!email.includes('@')) {
      newErrors.email = 'Email should contain an "@" symbol';
    }

    if (password.length < 6) {
      newErrors.password = 'Password should be at least 6 characters';
    }

    setErrors(newErrors);

    return Object.values(newErrors).every((error) => error === '');
  };

  const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault();

    if (validateForm()) {
      setFormData(`Username: ${username}, Email: ${email}`);
      setIsSubmitted(true);
    }
  };

  const handleClearForm = () => {
    setUsername('');
    setEmail('');
    setPassword('');
    setErrors({
      username: '',
      email: '',
      password: '',
    });
    setIsSubmitted(false);
    setFormData('');
  };

  return (
    <div className="max-w-md mx-auto p-4 bg-white rounded-lg shadow-md">
      <h2 className="text-lg font-bold mb-4">Signup Form</h2>
      <form onSubmit={handleSubmit}>
        <div className="mb-4">
          <label className="block text-gray-700 text-sm font-bold mb-2" htmlFor="username">
            Username
          </label>
          <input
            className={`w-full p-2 border border-gray-400 rounded-lg focus:outline-none focus:border-blue-500 ${errors.username && 'border-red-500'}`}
            type="text"
            id="username"
            value={username}
            onChange={(e) => setUsername(e.target.value)}
          />
          {errors.username && <p className="text-red-500 text-sm mt-2">{errors.username}</p>}
        </div>
        <div className="mb-4">
          <label className="block text-gray-700 text-sm font-bold mb-2" htmlFor="email">
            Email
          </label>
          <input
            className={`w-full p-2 border border-gray-400 rounded-lg focus:outline-none focus:border-blue-500 ${errors.email && 'border-red-500'}`}
            type="text"
            id="email"
            value={email}
            onChange={(e) => setEmail(e.target.value)}
          />
          {errors.email && <p className="text-red-500 text-sm mt-2">{errors.email}</p>}
        </div>
        <div className="mb-4">
          <label className="block text-gray-700 text-sm font-bold mb-2" htmlFor="password">
            Password
          </label>
          <input
            className={`w-full p-2 border border-gray-400 rounded-lg focus:outline-none focus:border-blue-500 ${errors.password && 'border-red-500'}`}
            type="password"
            id="password"
            value={password}
            onChange={(e) => setPassword(e.target.value)}
          />
          {errors.password && <p className="text-red-500 text-sm mt-2">{errors.password}</p>}
        </div>
        <button
          className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-lg focus:outline-none focus:shadow-outline"
          type="submit"
        >
          Submit
        </button>
        <button
          className="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-lg focus:outline-none focus:shadow-outline ml-2"
          type="button"
          onClick={handleClearForm}
        >
          Clear Form
        </button>
      </form>
      {isSubmitted && <p className="text-lg font-bold mt-4">{formData}</p>}
    </div>
  );
};

export default SignupForm;
