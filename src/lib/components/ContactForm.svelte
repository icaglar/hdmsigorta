<script lang="ts">
	let formData = $state({
		name: '',
		phone: '',
		email: '',
		insuranceType: '',
		message: '',
		kvkk: false
	});

	let formStatus = $state<'idle' | 'submitting' | 'success' | 'error'>('idle');
	let errors = $state<Record<string, string>>({});

	const insuranceTypes = [
		'Kasko Sigortası',
		'Trafik Sigortası',
		'Sağlık Sigortası',
		'Konut Sigortası',
		'DASK',
		'Seyahat Sigortası',
		'Hayat Sigortası',
		'Kurumsal Sigorta'
	];

	function validate(): boolean {
		const e: Record<string, string> = {};

		if (!formData.name.trim()) e.name = 'Ad Soyad gereklidir.';
		if (!formData.phone.trim()) e.phone = 'Telefon gereklidir.';
		else if (!/^[0-9\s\-\+\(\)]{10,15}$/.test(formData.phone.trim())) e.phone = 'Geçerli bir telefon numarası girin.';
		if (!formData.email.trim()) e.email = 'E-posta gereklidir.';
		else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.email.trim())) e.email = 'Geçerli bir e-posta adresi girin.';
		if (!formData.insuranceType) e.insuranceType = 'Sigorta türü seçin.';
		if (!formData.kvkk) e.kvkk = 'KVKK onayı gereklidir.';

		errors = e;
		return Object.keys(e).length === 0;
	}

	async function handleSubmit(e: Event) {
		e.preventDefault();
		if (!validate()) return;

		formStatus = 'submitting';

		try {
			const res = await fetch('https://formsubmit.co/ajax/info@hdmsigorta.com', {
				method: 'POST',
				headers: { 'Content-Type': 'application/json', Accept: 'application/json' },
				body: JSON.stringify({
					'Ad Soyad': formData.name,
					Telefon: formData.phone,
					'E-posta': formData.email,
					'Sigorta Türü': formData.insuranceType,
					Mesaj: formData.message,
					_subject: `Yeni Teklif Talebi - ${formData.insuranceType}`
				})
			});

			if (res.ok) {
				formStatus = 'success';
				formData = { name: '', phone: '', email: '', insuranceType: '', message: '', kvkk: false };
			} else {
				formStatus = 'error';
			}
		} catch {
			formStatus = 'error';
		}

		setTimeout(() => {
			if (formStatus !== 'idle') formStatus = 'idle';
		}, 5000);
	}
</script>

<section id="iletisim" class="py-20 lg:py-28 bg-white">
	<div class="max-w-7xl mx-auto px-6">
		<div class="text-center mb-16" data-aos="fade-up">
			<span class="inline-block text-sm font-semibold text-teal-700 bg-teal-50 px-4 py-1.5 rounded-full mb-4">İLETİŞİM</span>
			<h2 class="font-heading font-bold text-3xl sm:text-4xl lg:text-[40px] text-charcoal-800 mb-4">
				Hızlı Teklif Alın
			</h2>
			<p class="text-charcoal-500 max-w-2xl mx-auto text-lg">
				Formu doldurun, en kısa sürede size en uygun teklifi iletelim.
			</p>
		</div>

		<div class="grid lg:grid-cols-5 gap-8 lg:gap-12" data-aos="fade-up" data-aos-delay="100">
			<!-- Form -->
			<div class="lg:col-span-3">
				<form onsubmit={handleSubmit} class="space-y-5" novalidate>
					<div class="grid sm:grid-cols-2 gap-5">
						<div>
							<label for="name" class="block text-sm font-medium text-charcoal-700 mb-1.5">Ad Soyad *</label>
							<input
								type="text"
								id="name"
								bind:value={formData.name}
								class="w-full px-4 py-3 border border-charcoal-200 rounded-xl focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition-all text-charcoal-800"
								placeholder="Adınız Soyadınız"
							/>
							{#if errors.name}<p class="text-red-500 text-sm mt-1">{errors.name}</p>{/if}
						</div>
						<div>
							<label for="phone" class="block text-sm font-medium text-charcoal-700 mb-1.5">Telefon *</label>
							<input
								type="tel"
								id="phone"
								bind:value={formData.phone}
								class="w-full px-4 py-3 border border-charcoal-200 rounded-xl focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition-all text-charcoal-800"
								placeholder="0 (5XX) XXX XX XX"
							/>
							{#if errors.phone}<p class="text-red-500 text-sm mt-1">{errors.phone}</p>{/if}
						</div>
					</div>

					<div class="grid sm:grid-cols-2 gap-5">
						<div>
							<label for="email" class="block text-sm font-medium text-charcoal-700 mb-1.5">E-posta *</label>
							<input
								type="email"
								id="email"
								bind:value={formData.email}
								class="w-full px-4 py-3 border border-charcoal-200 rounded-xl focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition-all text-charcoal-800"
								placeholder="ornek@email.com"
							/>
							{#if errors.email}<p class="text-red-500 text-sm mt-1">{errors.email}</p>{/if}
						</div>
						<div>
							<label for="type" class="block text-sm font-medium text-charcoal-700 mb-1.5">Sigorta Türü *</label>
							<select
								id="type"
								bind:value={formData.insuranceType}
								class="w-full px-4 py-3 border border-charcoal-200 rounded-xl focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition-all text-charcoal-800 bg-white"
							>
								<option value="">Seçiniz</option>
								{#each insuranceTypes as type}
									<option value={type}>{type}</option>
								{/each}
							</select>
							{#if errors.insuranceType}<p class="text-red-500 text-sm mt-1">{errors.insuranceType}</p>{/if}
						</div>
					</div>

					<div>
						<label for="message" class="block text-sm font-medium text-charcoal-700 mb-1.5">Mesajınız</label>
						<textarea
							id="message"
							bind:value={formData.message}
							rows="4"
							class="w-full px-4 py-3 border border-charcoal-200 rounded-xl focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition-all text-charcoal-800 resize-none"
							placeholder="Teklif almak istediğiniz detayları yazabilirsiniz..."
						></textarea>
					</div>

					<!-- KVKK -->
					<div>
						<label class="flex items-start gap-3 cursor-pointer">
							<input
								type="checkbox"
								bind:checked={formData.kvkk}
								class="mt-1 w-4 h-4 rounded border-charcoal-300 text-teal-700 focus:ring-teal-500"
							/>
							<span class="text-sm text-charcoal-500">
								<a href="#" class="text-teal-700 underline">KVKK Aydınlatma Metni</a>'ni okudum, kişisel verilerimin işlenmesini kabul ediyorum. *
							</span>
						</label>
						{#if errors.kvkk}<p class="text-red-500 text-sm mt-1">{errors.kvkk}</p>{/if}
					</div>

					<!-- Submit -->
					<button
						type="submit"
						disabled={formStatus === 'submitting'}
						class="w-full sm:w-auto bg-gold-500 hover:bg-gold-600 disabled:opacity-50 text-white font-semibold px-8 py-4 rounded-xl transition-all hover:shadow-lg hover:shadow-gold-500/25 flex items-center justify-center gap-2"
					>
						{#if formStatus === 'submitting'}
							<svg class="animate-spin w-5 h-5" fill="none" viewBox="0 0 24 24"><circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"/><path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4z"/></svg>
							Gönderiliyor...
						{:else}
							<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/></svg>
							Teklif Talep Et
						{/if}
					</button>

					<!-- Status messages -->
					{#if formStatus === 'success'}
						<div class="bg-green-50 border border-green-200 text-green-700 px-4 py-3 rounded-xl text-sm">
							Mesajınız başarıyla iletildi! En kısa sürede size dönüş yapacağız.
						</div>
					{/if}
					{#if formStatus === 'error'}
						<div class="bg-red-50 border border-red-200 text-red-700 px-4 py-3 rounded-xl text-sm">
							Bir hata oluştu. Lütfen tekrar deneyin veya bizi telefonla arayın.
						</div>
					{/if}
				</form>
			</div>

			<!-- Contact card -->
			<div class="lg:col-span-2">
				<div class="bg-teal-900 text-white rounded-2xl p-8 lg:p-10 h-full">
					<h3 class="font-heading font-bold text-xl mb-6">Bize Ulaşın</h3>

					<div class="space-y-6">
						<div class="flex items-start gap-4">
							<div class="w-10 h-10 bg-white/10 rounded-xl flex items-center justify-center shrink-0">
								<svg class="w-5 h-5 text-gold-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"/></svg>
							</div>
							<div>
								<div class="text-sm text-white/60 mb-1">Telefon</div>
								<a href="tel:+902121234567" class="hover:text-gold-400 transition-colors">(0212) 123 45 67</a>
							</div>
						</div>

						<div class="flex items-start gap-4">
							<div class="w-10 h-10 bg-whatsapp/20 rounded-xl flex items-center justify-center shrink-0">
								<svg class="w-5 h-5 text-whatsapp" fill="currentColor" viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
							</div>
							<div>
								<div class="text-sm text-white/60 mb-1">WhatsApp</div>
								<a href="https://wa.me/905321234567" target="_blank" rel="noopener" class="hover:text-whatsapp transition-colors">0 (532) 123 45 67</a>
							</div>
						</div>

						<div class="flex items-start gap-4">
							<div class="w-10 h-10 bg-white/10 rounded-xl flex items-center justify-center shrink-0">
								<svg class="w-5 h-5 text-gold-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/></svg>
							</div>
							<div>
								<div class="text-sm text-white/60 mb-1">E-posta</div>
								<a href="mailto:info@hdmsigorta.com" class="hover:text-gold-400 transition-colors">info@hdmsigorta.com</a>
							</div>
						</div>

						<div class="flex items-start gap-4">
							<div class="w-10 h-10 bg-white/10 rounded-xl flex items-center justify-center shrink-0">
								<svg class="w-5 h-5 text-gold-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"/><path d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"/></svg>
							</div>
							<div>
								<div class="text-sm text-white/60 mb-1">Adres</div>
								<p class="text-white/90 text-sm leading-relaxed">Levent Mah. Sigorta Cad. No:42/A<br/>Beşiktaş / İstanbul</p>
							</div>
						</div>

						<div class="flex items-start gap-4">
							<div class="w-10 h-10 bg-white/10 rounded-xl flex items-center justify-center shrink-0">
								<svg class="w-5 h-5 text-gold-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>
							</div>
							<div>
								<div class="text-sm text-white/60 mb-1">Çalışma Saatleri</div>
								<p class="text-white/90 text-sm">Pzt - Cuma: 09:00 - 18:00</p>
								<p class="text-white/90 text-sm">Cumartesi: 10:00 - 14:00</p>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>
