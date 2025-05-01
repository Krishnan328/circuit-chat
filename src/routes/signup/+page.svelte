<script lang="ts">
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';
	import { createClient } from '@supabase/supabase-js';
	
	// Initialize Supabase client
	// In a real app, these would be env variables
	const supabaseUrl = 'https://xpisgetbwxkdfevllwsq.supabase.co';
	const supabaseKey = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InhwaXNnZXRid3hrZGZldmxsd3NxIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NDU2ODg1NjIsImV4cCI6MjA2MTI2NDU2Mn0.IB9K5WH_13qXFLIDtLA6Q4_I8MCoiqTVRHWkrzisM-M';
	const supabase = createClient(supabaseUrl, supabaseKey);
	
	// Form state
	let fullName = '';
	let email = '';
	let username = '';
	let password = '';
	let confirmPassword = '';
	let loading = false;
	let errorMessage = '';

	onMount(() => {
		const shapes = document.querySelectorAll('.shape');

		shapes.forEach((shape) => {
			let posX = Math.random() * window.innerWidth;
			let posY = Math.random() * window.innerHeight;
			let speedX = (Math.random() - 0.5) * 3.5; // Increased speed
			let speedY = (Math.random() - 0.5) * 3.5; // Increased speed

			setInterval(() => {
				posX += speedX;
				posY += speedY;

				// Bounce off edges
				if (posX <= 0 || posX >= window.innerWidth - 200) {
					speedX *= -1;
				}
				if (posY <= 0 || posY >= window.innerHeight - 200) {
					speedY *= -1;
				}

				// Fix TypeScript error with type assertion
				(shape as HTMLElement).style.left = posX + 'px';
				(shape as HTMLElement).style.top = posY + 'px';
			}, 30);
		});
	});

	async function handleSignup() {
		// Validation
		if (!fullName || !email || !username || !password || !confirmPassword) {
			errorMessage = 'All fields are required';
			return;
		}
		
		if (password !== confirmPassword) {
			errorMessage = 'Passwords do not match';
			return;
		}
		
		// Min password length check
		if (password.length < 6) {
			errorMessage = 'Password must be at least 6 characters long';
			return;
		}
		
		try {
			loading = true;
			errorMessage = '';
			
			// Sign up with email and password
			const { data, error } = await supabase.auth.signUp({
				email,
				password,
				options: {
					data: {
						full_name: fullName,
						username
					}
				}
			});
			
			if (error) throw error;
			
			if (data?.user) {
				// Successfully signed up
				alert('Signup successful! Check your email for confirmation.');
				goto('/login'); // Redirect to login page
			}
		} catch (error) {
			// TypeScript type guard for error handling
			if (error instanceof Error) {
				errorMessage = error.message;
			} else {
				errorMessage = 'An unexpected error occurred';
			}
		} finally {
			loading = false;
		}
	}
	
	async function signInWithGoogle() {
		try {
			loading = true;
			errorMessage = '';
			const { error } = await supabase.auth.signInWithOAuth({
				provider: 'google'
			});
			
			if (error) throw error;
		} catch (error) {
			if (error instanceof Error) {
				errorMessage = error.message;
			} else {
				errorMessage = 'Failed to sign in with Google';
			}
		} finally {
			loading = false;
		}
	}
	
	async function signInWithFacebook() {
		try {
			loading = true;
			errorMessage = '';
			const { error } = await supabase.auth.signInWithOAuth({
				provider: 'facebook'
			});
			
			if (error) throw error;
		} catch (error) {
			if (error instanceof Error) {
				errorMessage = error.message;
			} else {
				errorMessage = 'Failed to sign in with Facebook';
			}
		} finally {
			loading = false;
		}
	}
</script>

<div class="background">
	<div class="shape"></div>
	<div class="shape"></div>
	<div class="shape"></div>
	<div class="shape"></div>
	<div class="shape"></div>
</div>
<form on:submit|preventDefault={handleSignup}>
	<h3>Create Account</h3>

	{#if errorMessage}
		<div class="error-message">{errorMessage}</div>
	{/if}

	<label for="fullname">Full Name</label>
	<input type="text" placeholder="Enter your full name" id="fullname" bind:value={fullName} />

	<label for="email">Email</label>
	<input type="email" placeholder="Enter your email" id="email" bind:value={email} />

	<label for="username">Username</label>
	<input type="text" placeholder="Choose a username" id="username" bind:value={username} />

	<label for="password">Password</label>
	<input type="password" placeholder="Create password" id="password" bind:value={password} />

	<label for="confirm-password">Confirm Password</label>
	<input type="password" placeholder="Confirm password" id="confirm-password" bind:value={confirmPassword} />

	<button type="submit" disabled={loading}>
		{loading ? 'Signing up...' : 'Sign Up'}
	</button>

	<div class="login-link">
		Already have an account? <a href="/login">Log In</a>
	</div>

	<div class="social">
		<div class="go" on:click={signInWithGoogle}>
			<i class="fab fa-google"></i> Google
		</div>
		<div class="fb" on:click={signInWithFacebook}>
			<i class="fab fa-facebook"></i> Facebook
		</div>
	</div>
</form>

<style>
	*,
	*:before,
	*:after {
		padding: 0;
		margin: 0;
		box-sizing: border-box;
	}

	:global(body) {
		background-color: #1e1e2e; /* Catppuccin Mocha base */
	}

	.background {
		width: 100%;
		height: 100vh;
		position: fixed;
		z-index: -1;
	}

	.background .shape {
		height: 200px;
		width: 200px;
		position: absolute;
		border-radius: 50%;
		filter: blur(15px);
		opacity: 0.8;
		transition: all 0.5s ease;
	}

	.shape:nth-child(1) {
		background: linear-gradient(#f5c2e7, /* Catppuccin Pink */ #cba6f7 /* Catppuccin Mauve */);
	}

	.shape:nth-child(2) {
		background: linear-gradient(#89dceb, /* Catppuccin Sky */ #74c7ec /* Catppuccin Sapphire */);
	}

	.shape:nth-child(3) {
		background: linear-gradient(#a6e3a1, /* Catppuccin Green */ #94e2d5 /* Catppuccin Teal */);
		height: 150px;
		width: 150px;
	}

	.shape:nth-child(4) {
		background: linear-gradient(#fab387, /* Catppuccin Peach */ #f9e2af /* Catppuccin Yellow */);
		height: 180px;
		width: 180px;
	}

	.shape:nth-child(5) {
		background: linear-gradient(#b4befe, /* Catppuccin Lavender */ #f5c2e7 /* Catppuccin Pink */);
		height: 170px;
		width: 170px;
	}

	form {
		height: 750px; /* Increased height for additional fields */
		width: 400px;
		background-color: rgba(30, 30, 46, 0.75);
		position: absolute;
		transform: translate(-50%, -50%);
		top: 50%;
		left: 50%;
		border-radius: 10px;
		backdrop-filter: blur(15px);
		border: 2px solid rgba(205, 214, 244, 0.1);
		box-shadow: 0 0 40px rgba(17, 17, 27, 0.6);
		padding: 50px 35px;
		z-index: 1;
		overflow-y: auto; /* Add scrolling for smaller screens */
	}

	form * {
		font-family: 'Poppins', sans-serif;
		color: #cdd6f4; /* Catppuccin Text */
		letter-spacing: 0.5px;
		outline: none;
		border: none;
	}

	form h3 {
		font-size: 32px;
		font-weight: 500;
		line-height: 42px;
		text-align: center;
		color: #f5c2e7; /* Catppuccin Pink */
	}

	label {
		display: block;
		margin-top: 20px; /* Reduced from 30px to fit more fields */
		font-size: 16px;
		font-weight: 500;
	}

	input {
		display: block;
		height: 50px;
		width: 100%;
		background-color: rgba(49, 50, 68, 0.7); /* Catppuccin Surface0 */
		border-radius: 8px;
		padding: 0 10px;
		margin-top: 8px;
		font-size: 14px;
		font-weight: 300;
		border: 1px solid rgba(108, 112, 134, 0.3); /* Catppuccin overlay0 */
	}

	input:focus {
		border: 1px solid #b4befe; /* Catppuccin Lavender */
	}

	::placeholder {
		color: #a6adc8; /* Catppuccin Subtext0 */
	}

	button {
		margin-top: 30px; /* Reduced from 50px */
		width: 100%;
		background-color: #cba6f7; /* Catppuccin Mauve */
		color: #1e1e2e; /* Catppuccin Base */
		padding: 15px 0;
		font-size: 18px;
		font-weight: 600;
		border-radius: 8px;
		cursor: pointer;
		transition: all 0.3s ease;
	}

	button:hover:not(:disabled) {
		background-color: #f5c2e7; /* Catppuccin Pink */
	}
	
	button:disabled {
		opacity: 0.7;
		cursor: not-allowed;
	}
	
	.error-message {
		background-color: rgba(243, 139, 168, 0.2); /* Catppuccin Red with opacity */
		color: #f38ba8; /* Catppuccin Red */
		padding: 10px;
		border-radius: 8px;
		margin-top: 15px;
		text-align: center;
		font-size: 14px;
	}

	.login-link {
		margin-top: 15px;
		text-align: center;
		font-size: 14px;
	}

	.login-link a {
		color: #b4befe; /* Catppuccin Lavender */
		text-decoration: none;
		font-weight: 500;
	}

	.login-link a:hover {
		text-decoration: underline;
	}

	.social {
		margin-top: 20px; /* Reduced from 30px */
		display: flex;
	}

	.social div {
		width: 150px;
		border-radius: 8px;
		padding: 8px 10px;
		background-color: rgba(49, 50, 68, 0.7); /* Catppuccin Surface0 */
		color: #cdd6f4; /* Catppuccin Text */
		text-align: center;
		cursor: pointer;
		transition: all 0.3s ease;
	}

	.social div:hover {
		background-color: rgba(69, 71, 90, 0.7); /* Catppuccin Surface1 */
	}

	.social .fb {
		margin-left: 25px;
	}

	.social i {
		margin-right: 4px;
	}
</style>