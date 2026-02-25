const LOGIN_PAGE = '/html/login.html';
const CATALOGUE_PAGE = '/html/catalogue.html';
const DETAILS_PAGE = '/html/filmdetails.html';

window.addEventListener('scroll', () => {
  const navbar = document.getElementById('navbar');
  if (!navbar) return;
  if (window.scrollY > 50) navbar.classList.add('scrolled');
  else navbar.classList.remove('scrolled');
});

document.addEventListener('DOMContentLoaded', () => {
  checkAuthAndLoadRentals();
});

async function checkAuthAndLoadRentals() {
  try {
    const response = await fetch(`${API_BASE_URL}/api/profil`, {
      credentials: 'include'
    });

    if (response.status === 401) {
      window.location.href = LOGIN_PAGE;
      return;
    }

    if (!response.ok) {
      window.location.href = LOGIN_PAGE;
      return;
    }

    await loadRentals();
  } catch (e) {
    console.error('Erreur auth:', e);
    window.location.href = LOGIN_PAGE;
  }
}

/**
 * ✅ IMPORTANT :
 * Si ton backend n'a pas exactement /api/rentals,
 * change RENTALS_ENDPOINT ici uniquement.
 */
const RENTALS_ENDPOINT = `${API_BASE_URL}/api/rentals`;

async function loadRentals() {
  const container = document.getElementById('rentals-content');
  if (!container) return;

  container.innerHTML = `<div class="loading">Chargement de vos locations...</div>`;

  try {
    const response = await fetch(RENTALS_ENDPOINT, {
      credentials: 'include'
    });

    if (response.status === 401) {
      window.location.href = LOGIN_PAGE;
      return;
    }

    const result = await response.json().catch(() => ({}));

    if (!response.ok || !result.success) {
      showError(result.message || `Erreur lors du chargement des locations (HTTP ${response.status})`);
      return;
    }

    // result.data = tableau de locations
    renderRentals(result.data || []);
  } catch (e) {
    console.error('Erreur rentals:', e);
    showError("Erreur lors du chargement de vos locations.");
  }
}

function renderRentals(rentals) {
  const container = document.getElementById('rentals-content');
  if (!container) return;

  if (!rentals || rentals.length === 0) {
    container.innerHTML = `
      <div class="empty">
        <h3>Aucune location</h3>
        <p>Vous n'avez pas encore loué de film.</p>
        <a class="btn btn-secondary" href="${CATALOGUE_PAGE}">Aller au catalogue</a>
      </div>
    `;
    return;
  }

  // Exemple de tri: les locations actives d'abord (si champ returned_at existe)
  const sorted = [...rentals].sort((a, b) => {
    const aReturned = !!(a.returned_at || a.date_retour);
    const bReturned = !!(b.returned_at || b.date_retour);
    return (aReturned === bReturned) ? 0 : (aReturned ? 1 : -1);
  });

  container.innerHTML = `
    <div class="rentals-grid">
      ${sorted.map(r => rentalCardHTML(r)).join('')}
    </div>
  `;

  // Attacher handlers
  sorted.forEach(r => {
    const filmId = getFilmId(r);
    const btn = document.getElementById(`details-${r.id}`);
    if (btn && filmId) {
      btn.addEventListener('click', (e) => {
        e.preventDefault();
        window.location.href = `${DETAILS_PAGE}?id=${filmId}`;
      });
    }
  });
}

function rentalCardHTML(r) {
  const film = r.film || r.film_details || null;

  const filmTitle = film?.title || r.title || 'Titre inconnu';
  const filmYear = film?.annee_sortie || r.annee_sortie || '';
  const filmGenre = (film?.genre || r.genre || '').split(',')[0]?.trim() || '';
  const imgPath = film?.imgPath || film?.imgpath || r.imgPath || r.imgpath || null;

  const dateLocation = formatDate(r.rented_at || r.date_location || r.created_at);
  const dateRetour = formatDate(r.returned_at || r.date_retour);

  const isReturned = !!(r.returned_at || r.date_retour);
  const statusLabel = isReturned ? 'Retourné' : 'En cours';
  const statusClass = isReturned ? 'returned' : 'active';

  const posterFallback = `
    <div style="text-align:center;color:#e7f4ff;padding:1rem;">
      <div style="font-size:2.3rem;margin-bottom:0.5rem;">🎬</div>
      <div style="font-size:0.8rem;text-transform:uppercase;letter-spacing:1px;">
        ${filmGenre || 'Film'}
      </div>
    </div>
  `;

  return `
    <div class="rental-card">
      <div class="rental-thumb">
        ${imgPath
          ? `<img src="${imgPath}" alt="${filmTitle}"
                 onerror="this.style.display='none'; this.parentElement.innerHTML=\`${posterFallback}\`;">`
          : posterFallback
        }
        <div class="rental-status ${statusClass}">${statusLabel}</div>
      </div>

      <div class="rental-body">
        <h3 class="rental-title">${filmTitle}</h3>
        <div class="rental-meta">
          <span>${filmYear || 'N/A'}</span>
          <span>${filmGenre}</span>
        </div>

        <div class="rental-dates">
          <div><strong>Loué :</strong> ${dateLocation || 'N/A'}</div>
          <div><strong>Retour :</strong> ${dateRetour || (isReturned ? 'N/A' : 'Non retourné')}</div>
        </div>

        <div class="rental-actions">
          <a href="#" class="btn btn-secondary" id="details-${r.id}">Détails</a>
        </div>
      </div>
    </div>
  `;
}

function getFilmId(r) {
  return r.film_id || r.filmId || r.film?.id || null;
}

function formatDate(d) {
  if (!d) return '';
  const date = new Date(d);
  if (Number.isNaN(date.getTime())) return '';
  return date.toLocaleDateString('fr-FR', { year: 'numeric', month: 'short', day: 'numeric' });
}

function showError(message) {
  const container = document.getElementById('rentals-content');
  if (!container) return;

  container.innerHTML = `
    <div class="error">
      ${message}
      <div class="error-actions">
        <a href="${CATALOGUE_PAGE}" class="btn btn-secondary">Retour au catalogue</a>
      </div>
    </div>
  `;
}

// ✅ Logout robuste (évite crash si bouton absent)
const logoutBtn = document.getElementById('logout-btn');
if (logoutBtn) {
  logoutBtn.addEventListener('click', async () => {
    try { await fetch(`${API_BASE_URL}/api/auth/logout`, { credentials: 'include' }); }
    catch (e) { console.error('Erreur déconnexion:', e); }
    finally { window.location.href = LOGIN_PAGE; }
  });
}
