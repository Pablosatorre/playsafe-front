<script lang="ts">
	import LogoHorizontal from '$lib/assets/images/logo-horizontal.svelte';
	import BackgroundImage from '$lib/assets/images/login-background2.jpg';
	import {
		FieldGroup,
		Field,
		FieldLabel,
		FieldDescription,
		FieldSeparator
	} from '$lib/components/ui/field/index.js';
	import { Input } from '$lib/components/ui/input/index.js';
	import { Button } from '$lib/components/ui/button/index.js';
	import { Card, CardContent, CardHeader } from '$lib/components/ui/card/index.js';
	import { Checkbox } from '$lib/components/ui/checkbox/index.js';

	// Wizard state
	let currentStep = 1;
	const totalSteps = 3;

	// Form data
	let email = '';
	let password = '';
	let confirmPassword = '';
	let firstName = '';
	let lastName = '';
	let acceptTerms = false;

	// Password strength
	$: passwordStrength = calculatePasswordStrength(password);

	function calculatePasswordStrength(pwd: string): number {
		if (!pwd) return 0;
		let strength = 0;
		if (pwd.length >= 8) strength++;
		if (pwd.length >= 12) strength++;
		if (/[a-z]/.test(pwd) && /[A-Z]/.test(pwd)) strength++;
		if (/[0-9]/.test(pwd)) strength++;
		if (/[^a-zA-Z0-9]/.test(pwd)) strength++;
		return Math.min(strength, 4);
	}

	$: strengthColor =
		passwordStrength === 0
			? 'bg-border'
			: passwordStrength === 1
				? 'bg-red-500'
				: passwordStrength === 2
					? 'bg-orange-500'
					: passwordStrength === 3
						? 'bg-yellow-500'
						: 'bg-green-500';

	$: strengthText =
		passwordStrength === 0
			? ''
			: passwordStrength === 1
				? 'Weak'
				: passwordStrength === 2
					? 'Fair'
					: passwordStrength === 3
						? 'Good'
						: 'Strong';

	// Navigation functions
	function nextStep() {
		if (currentStep < totalSteps) {
			currentStep++;
		}
	}

	function prevStep() {
		if (currentStep > 1) {
			currentStep--;
		}
	}

	function handleSubmit(e: Event) {
		e.preventDefault();
		if (currentStep < totalSteps) {
			nextStep();
		} else {
			// Submit form
			console.log('Form submitted');
		}
	}

	// Progress percentage
	$: progress = (currentStep / totalSteps) * 100;
</script>

<svelte:head>
	<title>Sign Up - PlaySafe</title>
</svelte:head>

<div class="flex min-h-svh lg:grid lg:grid-cols-2">
	<div class="flex flex-col gap-4 p-6 md:p-8 w-full">
		<div class="flex justify-center gap-2 md:justify-start">
			<a href="/" class="flex items-center gap-2 font-medium transition-opacity hover:opacity-80">
				<LogoHorizontal />
			</a>
		</div>
		<div class="flex flex-1 items-center justify-center">
			<Card class="w-full max-w-md border-border/50 shadow-2xl backdrop-blur">
				<CardHeader class="space-y-2 pb-3 pt-5">
					<div class="flex flex-col items-center gap-2 text-center">
						<div
							class="rounded-2xl bg-gradient-to-br from-primary/20 to-primary/5 p-2.5 mb-1 ring-1 ring-primary/10"
						>
							<svg
								xmlns="http://www.w3.org/2000/svg"
								fill="none"
								viewBox="0 0 24 24"
								stroke-width="1.5"
								stroke="currentColor"
								class="w-7 h-7 text-primary"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									d="M19 7.5v3m0 0v3m0-3h3m-3 0h-3m-2.25-4.125a3.375 3.375 0 11-6.75 0 3.375 3.375 0 016.75 0zM4 19.235v-.11a6.375 6.375 0 0112.75 0v.109A12.318 12.318 0 0110.374 21c-2.331 0-4.512-.645-6.374-1.766z"
								/>
							</svg>
						</div>
						<div class="space-y-1">
							<h1
								class="text-2xl font-bold tracking-tight bg-gradient-to-r from-foreground to-foreground/70 bg-clip-text"
							>
								Create your account
							</h1>
							<p class="text-muted-foreground text-balance text-sm">
								Step {currentStep} of {totalSteps}
							</p>
						</div>
					</div>

					<!-- Progress Bar -->
					<div class="w-full bg-border/30 rounded-full h-1.5 overflow-hidden mt-4">
						<div
							class="bg-primary h-full transition-all duration-300 ease-out"
							style="width: {progress}%"
						></div>
					</div>

					<!-- Step Indicators -->
					<div class="flex justify-center gap-2 pt-2">
						{#each Array(totalSteps) as _, i}
							<div
								class="flex items-center gap-2 text-xs font-medium transition-all"
								class:text-primary={currentStep === i + 1}
								class:text-muted-foreground={currentStep !== i + 1}
							>
								<div
									class="w-6 h-6 rounded-full flex items-center justify-center border-2 transition-all"
									class:border-primary={currentStep >= i + 1}
									class:bg-primary={currentStep > i + 1}
									class:text-primary-foreground={currentStep > i + 1}
									class:border-border={currentStep < i + 1}
								>
									{#if currentStep > i + 1}
										<svg
											xmlns="http://www.w3.org/2000/svg"
											viewBox="0 0 20 20"
											fill="currentColor"
											class="w-3 h-3"
										>
											<path
												fill-rule="evenodd"
												d="M16.704 4.153a.75.75 0 01.143 1.052l-8 10.5a.75.75 0 01-1.127.075l-4.5-4.5a.75.75 0 011.06-1.06l3.894 3.893 7.48-9.817a.75.75 0 011.05-.143z"
												clip-rule="evenodd"
											/>
										</svg>
									{:else}
										{i + 1}
									{/if}
								</div>
							</div>
						{/each}
					</div>
				</CardHeader>
				<CardContent class="pb-5">
					<form class="space-y-3.5" on:submit={handleSubmit}>
						<FieldGroup>
							<!-- Step 1: Email -->
							{#if currentStep === 1}
								<!-- Social Login Buttons -->
								<div class="grid grid-cols-2 gap-3">
									<Button
										variant="outline"
										type="button"
										class="w-full h-10 hover:bg-accent hover:border-primary/30 transition-all"
									>
										<svg
											xmlns="http://www.w3.org/2000/svg"
											viewBox="0 0 24 24"
											class="w-4 h-4 mr-2"
										>
											<path
												fill="currentColor"
												d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"
											/>
											<path
												fill="currentColor"
												d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"
											/>
											<path
												fill="currentColor"
												d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z"
											/>
											<path
												fill="currentColor"
												d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z"
											/>
										</svg>
										Google
									</Button>
									<Button
										variant="outline"
										type="button"
										class="w-full h-10 hover:bg-accent hover:border-primary/30 transition-all"
									>
										<svg
											xmlns="http://www.w3.org/2000/svg"
											viewBox="0 0 24 24"
											class="w-4 h-4 mr-2"
										>
											<path
												fill="currentColor"
												d="M20.317 4.37a19.791 19.791 0 0 0-4.885-1.515a.074.074 0 0 0-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 0 0-5.487 0a12.64 12.64 0 0 0-.617-1.25a.077.077 0 0 0-.079-.037A19.736 19.736 0 0 0 3.677 4.37a.07.07 0 0 0-.032.027C.533 9.046-.32 13.58.099 18.057a.082.082 0 0 0 .031.057a19.9 19.9 0 0 0 5.993 3.03a.078.078 0 0 0 .084-.028a14.09 14.09 0 0 0 1.226-1.994a.076.076 0 0 0-.041-.106a13.107 13.107 0 0 1-1.872-.892a.077.077 0 0 1-.008-.128a10.2 10.2 0 0 0 .372-.292a.074.074 0 0 1 .077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 0 1 .078.01c.12.098.246.198.373.292a.077.077 0 0 1-.006.127a12.299 12.299 0 0 1-1.873.892a.077.077 0 0 0-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 0 0 .084.028a19.839 19.839 0 0 0 6.002-3.03a.077.077 0 0 0 .032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 0 0-.031-.03zM8.02 15.33c-1.183 0-2.157-1.085-2.157-2.419c0-1.333.956-2.419 2.157-2.419c1.21 0 2.176 1.096 2.157 2.42c0 1.333-.956 2.418-2.157 2.418zm7.975 0c-1.183 0-2.157-1.085-2.157-2.419c0-1.333.955-2.419 2.157-2.419c1.21 0 2.176 1.096 2.157 2.42c0 1.333-.946 2.418-2.157 2.418z"
											/>
										</svg>
										Discord
									</Button>
								</div>

								<FieldSeparator class="my-3.5">Or continue with email</FieldSeparator>

								<div class="space-y-2.5">
									<Field>
										<FieldLabel for="email" class="text-sm font-medium">Email address</FieldLabel>
										<Input
											id="email"
											type="email"
											placeholder="you@example.com"
											bind:value={email}
											required
											class="h-10"
										/>
										<FieldDescription class="text-xs mt-1.5">
											We'll send you a verification email
										</FieldDescription>
									</Field>
								</div>
							{/if}

							<!-- Step 2: Name -->
							{#if currentStep === 2}
								<div class="space-y-2.5">
									<Field>
										<FieldLabel for="firstName" class="text-sm font-medium">First name</FieldLabel>
										<Input
											id="firstName"
											type="text"
											placeholder="John"
											bind:value={firstName}
											required
											class="h-10"
										/>
									</Field>
									<Field>
										<FieldLabel for="lastName" class="text-sm font-medium">Last name</FieldLabel>
										<Input
											id="lastName"
											type="text"
											placeholder="Doe"
											bind:value={lastName}
											required
											class="h-10"
										/>
									</Field>
								</div>
							{/if}

							<!-- Step 3: Password & Terms -->
							{#if currentStep === 3}
								<div class="space-y-2.5">
									<Field>
										<FieldLabel for="password" class="text-sm font-medium">Password</FieldLabel>
										<Input
											id="password"
											type="password"
											bind:value={password}
											required
											class="h-10"
										/>
										<FieldDescription class="text-xs mt-1.5">
											Must be at least 8 characters long
										</FieldDescription>
									</Field>
									<Field>
										<FieldLabel for="confirm-password" class="text-sm font-medium"
											>Confirm password</FieldLabel
										>
										<Input
											id="confirm-password"
											type="password"
											bind:value={confirmPassword}
											required
											class="h-10"
										/>
									</Field>

									<!-- Password strength indicator -->
									<div class="pt-2">
										<div class="flex items-center justify-between mb-2">
											<p class="text-xs text-muted-foreground">Password strength:</p>
											{#if password}
												<p
													class="text-xs font-medium"
													class:text-red-500={passwordStrength === 1}
													class:text-orange-500={passwordStrength === 2}
													class:text-yellow-500={passwordStrength === 3}
													class:text-green-500={passwordStrength === 4}
												>
													{strengthText}
												</p>
											{/if}
										</div>
										<div class="flex gap-1">
											{#each Array(4) as _, i}
												<div
													class="h-1.5 flex-1 rounded transition-colors"
													class:bg-red-500={passwordStrength >= 1 && i === 0}
													class:bg-orange-500={passwordStrength >= 2 && i === 1}
													class:bg-yellow-500={passwordStrength >= 3 && i === 2}
													class:bg-green-500={passwordStrength >= 4 && i === 3}
													class:bg-border={passwordStrength <= i}
												></div>
											{/each}
										</div>
									</div>

									<!-- Terms and Conditions -->
									<div class="flex items-start space-x-2 pt-3">
										<Checkbox id="terms" bind:checked={acceptTerms} class="mt-0.5" />
										<label
											for="terms"
											class="text-sm leading-tight text-muted-foreground cursor-pointer"
										>
											I agree to the
											<a
												href="/terms"
												class="text-primary font-medium hover:underline underline-offset-4"
											>
												Terms of Service
											</a>
											and
											<a
												href="/privacy"
												class="text-primary font-medium hover:underline underline-offset-4"
											>
												Privacy Policy
											</a>
										</label>
									</div>
								</div>
							{/if}

							<!-- Navigation Buttons -->
							<div
								class="grid gap-2 mt-4"
								class:grid-cols-2={currentStep > 1}
								class:grid-cols-1={currentStep === 1}
							>
								{#if currentStep > 1}
									<Button
										type="button"
										variant="outline"
										onclick={prevStep}
										class="h-10 text-sm font-medium"
									>
										<svg
											xmlns="http://www.w3.org/2000/svg"
											fill="none"
											viewBox="0 0 24 24"
											stroke-width="1.5"
											stroke="currentColor"
											class="w-4 h-4 mr-2"
										>
											<path
												stroke-linecap="round"
												stroke-linejoin="round"
												d="M15.75 19.5L8.25 12l7.5-7.5"
											/>
										</svg>
										Back
									</Button>
								{/if}
								<Button
									type="submit"
									class="h-10 text-sm font-medium shadow-lg shadow-primary/25 hover:shadow-xl hover:shadow-primary/30 transition-all"
								>
									{#if currentStep === totalSteps}
										<svg
											xmlns="http://www.w3.org/2000/svg"
											fill="none"
											viewBox="0 0 24 24"
											stroke-width="1.5"
											stroke="currentColor"
											class="w-4 h-4 mr-2 flex-shrink-0"
										>
											<path
												stroke-linecap="round"
												stroke-linejoin="round"
												d="M9 12.75L11.25 15 15 9.75m-3-7.036A11.959 11.959 0 013.598 6 11.99 11.99 0 003 9.749c0 5.592 3.824 10.29 9 11.623 5.176-1.332 9-6.03 9-11.622 0-1.31-.21-2.571-.598-3.751h-.152c-3.196 0-6.1-1.248-8.25-3.285z"
											/>
										</svg>
										<span>Create account</span>
									{:else}
										<span>Continue</span>
										<svg
											xmlns="http://www.w3.org/2000/svg"
											fill="none"
											viewBox="0 0 24 24"
											stroke-width="1.5"
											stroke="currentColor"
											class="w-4 h-4 ml-2 flex-shrink-0"
										>
											<path
												stroke-linecap="round"
												stroke-linejoin="round"
												d="M8.25 4.5l7.5 7.5-7.5 7.5"
											/>
										</svg>
									{/if}
								</Button>
							</div>

							<!-- Sign In Link -->
							<div class="relative mt-3.5">
								<div class="absolute inset-0 flex items-center">
									<div class="w-full border-t border-border/40"></div>
								</div>
								<div class="relative flex justify-center text-xs">
									<span class="bg-background px-3 text-muted-foreground">
										Already have an account?
									</span>
								</div>
							</div>

							<a
								href="/login"
								class="inline-flex items-center justify-center w-full h-10 px-4 rounded-md border border-dashed border-input bg-background text-sm font-medium hover:bg-accent hover:text-accent-foreground hover:border-solid transition-all"
							>
								<svg
									xmlns="http://www.w3.org/2000/svg"
									fill="none"
									viewBox="0 0 24 24"
									stroke-width="1.5"
									stroke="currentColor"
									class="w-4 h-4 mr-2 flex-shrink-0"
								>
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										d="M15.75 9V5.25A2.25 2.25 0 0013.5 3h-6a2.25 2.25 0 00-2.25 2.25v13.5A2.25 2.25 0 007.5 21h6a2.25 2.25 0 002.25-2.25V15m3 0l3-3m0 0l-3-3m3 3H9"
									/>
								</svg>
								<span>Sign in instead</span>
							</a>
						</FieldGroup>
					</form>
				</CardContent>
			</Card>
		</div>
	</div>
	<div class="bg-muted relative hidden lg:block overflow-hidden">
		<div
			class="absolute inset-0 bg-gradient-to-br from-primary/20 via-background/10 to-primary/10 z-10"
		></div>
		<img
			src={BackgroundImage}
			alt="Background"
			class="absolute inset-0 h-full w-full object-cover dark:opacity-40"
		/>
		<div class="absolute inset-0 flex items-center justify-center z-20 p-12">
			<div class="max-w-lg text-center space-y-6">
				<div
					class="inline-flex items-center justify-center p-4 rounded-full bg-primary/10 backdrop-blur-xl border border-primary/20 mb-4"
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke-width="1.5"
						stroke="currentColor"
						class="w-12 h-12 text-primary"
					>
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							d="M9 12.75L11.25 15 15 9.75m-3-7.036A11.959 11.959 0 013.598 6 11.99 11.99 0 003 9.749c0 5.592 3.824 10.29 9 11.623 5.176-1.332 9-6.03 9-11.622 0-1.31-.21-2.571-.598-3.751h-.152c-3.196 0-6.1-1.248-8.25-3.285z"
						/>
					</svg>
				</div>
				<div
					class="space-y-4 backdrop-blur-sm bg-background/30 p-8 rounded-2xl border border-primary/20"
				>
					<h2 class="text-4xl font-bold text-foreground leading-tight">
						Join Thousands of<br />Protected Servers
					</h2>
					<p class="text-lg text-foreground/80">
						Start protecting your game servers today with enterprise-grade DDoS protection and
						advanced security features.
					</p>
					<div class="flex items-center justify-center gap-8 pt-4">
						<div class="text-center">
							<div class="text-3xl font-bold text-primary">3</div>
							<div class="text-sm text-muted-foreground">Steps</div>
						</div>
						<div class="h-12 w-px bg-border"></div>
						<div class="text-center">
							<div class="text-3xl font-bold text-primary">2min</div>
							<div class="text-sm text-muted-foreground">Setup</div>
						</div>
						<div class="h-12 w-px bg-border"></div>
						<div class="text-center">
							<div class="text-3xl font-bold text-primary">∞</div>
							<div class="text-sm text-muted-foreground">Scalability</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>
