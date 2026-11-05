import React, { useState, useEffect, useRef, useCallback, useMemo } from 'react';
import {
  Instagram, ShoppingBag, Search, Menu, X, Settings, Plus, Edit2, Trash2,
  Upload, Save, LogOut, Package, Image as ImageIcon, RotateCcw, Eye,
  CheckCircle2, AlertCircle, Info, AlertTriangle, Sparkles, Home, ChefHat,
  Tag, Filter, ArrowLeft, ArrowDown, ArrowUp, Star, Loader2, Lock, Store, Palette,
  Link as LinkIcon, FileImage, Copy, Share2, Cloud, Database
} from 'lucide-react';

// ─── Types ───────────────────────────────────────────────
interface ProductDimensions {
  length?: number;
  width?: number;
  diameter?: number;
  height?: number;
}

type BadgeType = 'new' | 'sale' | 'restock' | 'none';

interface Product {
  id: string;
  name: string;
  description?: string;
  dimensions?: ProductDimensions;
  pieceCount?: number;
  price: string;
  oldPrice?: string;
  category: string;
  image: string;
  badge?: BadgeType;
  featured?: boolean;
}

const BADGE_OPTIONS: { value: BadgeType; label: string; className: string }[] = [
  { value: 'none', label: 'بدون شارة', className: '' },
  { value: 'new', label: 'جديد', className: 'bg-emerald-500/20 text-emerald-400 border border-emerald-500/40' },
  { value: 'sale', label: 'خصم', className: 'bg-rose-500/20 text-rose-400 border border-rose-500/40' },
  { value: 'restock', label: 'متوفر من جديد', className: 'bg-sky-500/20 text-sky-400 border border-sky-400/40' },
];

function getBadgeStyle(badge?: BadgeType): { label: string; className: string } | null {
  if (!badge || badge === 'none') return null;
  const opt = BADGE_OPTIONS.find((o) => o.value === badge);
  if (!opt) return null;
  return { label: opt.label, className: opt.className };
}

interface StoreSettings {
  logo: string | null;
  storeName: string;
  tagline: string;
  instagramUrl: string;
  heroTitle1: string;
  heroTitle2: string;
  categoryOrder: string[];
}

type ToastType = 'success' | 'error' | 'info' | 'warning';
interface ToastItem {
  id: string;
  type: ToastType;
  message: string;
}

// ─── Constants ───────────────────────────────────────────
const ALL_CATEGORIES = [
  { id: 'all', label: 'الكل', icon: Sparkles },
  { id: 'cookware', label: 'أواني الطهي', icon: ChefHat },
  { id: 'kitchen', label: 'أدوات المطبخ', icon: Package },
  { id: 'dining', label: 'أدوات المائدة', icon: Tag },
  { id: 'decor', label: 'ديكور المنزل', icon: Home },
];

const DEFAULT_CATEGORY_ORDER = ['cookware', 'kitchen', 'dining', 'decor'];

function getOrderedCategories(order?: string[]): typeof ALL_CATEGORIES {
  if (!order || order.length === 0) {
    return [ALL_CATEGORIES[0], ...ALL_CATEGORIES.slice(1)];
  }
  const ordered = order
    .map((id) => ALL_CATEGORIES.find((c) => c.id === id))
    .filter((c): c is typeof ALL_CATEGORIES[number] => !!c);
  const missing = ALL_CATEGORIES.filter((c) => c.id !== 'all' && !order.includes(c.id));
  return [ALL_CATEGORIES[0], ...ordered, ...missing];
}

const DEFAULT_PRODUCTS: Product[] = [
  {
    id: 'p1',
    name: 'طقم أواني ستانلس ستيل فاخر',
    description: 'طقم أواني فاخر مصنّع من أحدث خامات الستانلس ستيل المقاوم للصدأ بدرجة 18/10.',
    dimensions: { diameter: 24, height: 12 },
    pieceCount: 10,
    price: '459',
    oldPrice: '599',
    category: 'cookware',
    image: 'https://images.pexels.com/photos/36552082/pexels-photo-36552082.png?auto=compress&cs=tinysrgb&h=650&w=940',
    badge: 'sale',
    featured: true,
  },
];

const DEFAULT_SETTINGS: StoreSettings = {
  logo: null,
  storeName: 'GLOW_HOME',
  tagline: 'للأدوات المنزلية والمطبخ',
  instagramUrl: 'https://www.instagram.com/0_glow.home/',
  heroTitle1: 'اجعل منزلك ومطبخك يتألق',
  heroTitle2: 'بفخامة منتجات كلو هوم',
  categoryOrder: DEFAULT_CATEGORY_ORDER,
};

const STORAGE_KEYS = {
  adminPassword: 'glow_home_admin_password',
};

const DEFAULT_ADMIN_PASSWORD = 'glow2024';

function getAdminPassword(): string {
  try {
    const saved = localStorage.getItem(STORAGE_KEYS.adminPassword);
    return saved || DEFAULT_ADMIN_PASSWORD;
  } catch {
    return DEFAULT_ADMIN_PASSWORD;
  }
}

// ─── Simulated Cloud Sync (Local Storage Persistent) ─────
const CloudSync = {
  async getProducts(): Promise<Product[] | null> {
    try {
      const raw = localStorage.getItem('glow_home_cloud_products');
      return raw ? JSON.parse(raw) : null;
    } catch {
      return null;
    }
  },
  async saveProducts(products: Product[]): Promise<void> {
    try {
      localStorage.setItem('glow_home_cloud_products', JSON.stringify(products));
      localStorage.setItem('glow_home_products_v2', JSON.stringify(products));
    } catch (e) {
      console.error('Cloud save failed', e);
    }
  },
  async getSettings(): Promise<StoreSettings | null> {
    try {
      const raw = localStorage.getItem('glow_home_cloud_settings');
      return raw ? JSON.parse(raw) : null;
    } catch {
      return null;
    }
  },
  async saveSettings(settings: StoreSettings): Promise<void> {
    try {
      localStorage.setItem('glow_home_cloud_settings', JSON.stringify(settings));
      localStorage.setItem('glow_home_settings_v2', JSON.stringify(settings));
    } catch (e) {
      console.error('Settings cloud save failed', e);
    }
  }
};

// ─── Helpers ─────────────────────────────────────────────
async function compressImage(file: File, maxSize = 600, quality = 0.75): Promise<string> {
  return new Promise((resolve, reject) => {
    const reader = new FileReader();
    reader.onload = (e) => {
      const img = new Image();
      img.onload = () => {
        const canvas = document.createElement('canvas');
        let { width, height } = img;
        if (width > height && width > maxSize) {
          height = Math.round((height * maxSize) / width);
          width = maxSize;
        } else if (height > maxSize) {
          width = Math.round((width * maxSize) / height);
          height = maxSize;
        }
        canvas.width = width;
        canvas.height = height;
        const ctx = canvas.getContext('2d');
        if (!ctx) {
          resolve(e.target?.result as string);
          return;
        }
        ctx.drawImage(img, 0, 0, width, height);
        resolve(canvas.toDataURL('image/jpeg', quality));
      };
      img.onerror = reject;
      img.src = e.target?.result as string;
    };
    reader.onerror = reject;
    reader.readAsDataURL(file);
  });
}

function formatPrice(price: string | number): string {
  const str = String(price);
  const num = parseFloat(str);
  if (isNaN(num)) return `${str} د.ع`;
  return `${num.toLocaleString('en-US')} د.ع`;
}

function generateId(): string {
  return `p_${Date.now()}_${Math.random().toString(36).slice(2, 8)}`;
}

const DEFAULT_PRODUCT_IMAGE = "https://images.unsplash.com/photo-1556911220-e15b29be8c8f?auto=format&fit=crop&w=800&q=80";

const DIMENSION_LABELS: { key: keyof ProductDimensions; label: string }[] = [
  { key: 'length', label: 'الطول' },
  { key: 'width', label: 'العرض' },
  { key: 'diameter', label: 'القطر' },
  { key: 'height', label: 'الارتفاع' },
];

function getFilledDimensions(dims?: ProductDimensions): { label: string; value: number }[] {
  if (!dims) return [];
  return DIMENSION_LABELS
    .filter((d) => dims[d.key] != null && dims[d.key]! > 0)
    .map((d) => ({ label: d.label, value: dims[d.key]! }));
}

function buildOrderMessage(product: Product, settings: StoreSettings): string {
  return `مرحباً ${settings.storeName} 👋\nأرغب في طلب المنتج التالي:\n🛍️ المنتج: ${product.name}\n💰 السعر: ${formatPrice(product.price)}`;
}

async function copyToClipboard(text: string): Promise<boolean> {
  try {
    const textArea = document.createElement("textarea");
    textArea.value = text;
    document.body.appendChild(textArea);
    textArea.select();
    document.execCommand('copy');
    document.body.removeChild(textArea);
    return true;
  } catch {
    return false;
  }
}

// ─── Hooks ───────────────────────────────────────────────
function useToast() {
  const [toasts, setToasts] = useState<ToastItem[]>([]);
  const addToast = useCallback((type: ToastType, message: string) => {
    const id = `t_${Date.now()}_${Math.random().toString(36).slice(2, 6)}`;
    setToasts((prev) => [...prev, { id, type, message }]);
    setTimeout(() => {
      setToasts((prev) => prev.filter((t) => t.id !== id));
    }, 3500);
  }, []);
  const removeToast = useCallback((id: string) => {
    setToasts((prev) => prev.filter((t) => t.id !== id));
  }, []);
  return { toasts, addToast, removeToast };
}

// ─── Toast Container ─────────────────────────────────────
function ToastContainer({ toasts, onClose }: { toasts: ToastItem[]; onClose: (id: string) => void }) {
  const icons = {
    success: CheckCircle2,
    error: AlertCircle,
    info: Info,
    warning: AlertTriangle,
  };
  const colors = {
    success: 'border-emerald-500/30 bg-emerald-500/10 text-emerald-400',
    error: 'border-rose-500/30 bg-rose-500/10 text-rose-400',
    info: 'border-teal-500/30 bg-teal-500/10 text-teal-400',
    warning: 'border-amber-500/30 bg-amber-500/10 text-amber-400',
  };
  return (
    <div className="fixed top-6 left-1/2 -translate-x-1/2 z-[100] flex flex-col gap-3 w-full max-w-sm px-4 pointer-events-none">
      {toasts.map((toast) => {
        const Icon = icons[toast.type];
        return (
          <div
            key={toast.id}
            className={`bg-zinc-900/95 backdrop-blur-md rounded-2xl px-5 py-4 flex items-center gap-3 border ${colors[toast.type]} pointer-events-auto shadow-2xl`}
          >
            <Icon size={22} className="shrink-0" />
            <p className="text-sm font-medium text-zinc-100 flex-1 leading-relaxed">{toast.message}</p>
            <button onClick={() => onClose(toast.id)} className="text-zinc-500 hover:text-zinc-200 transition shrink-0">
              <X size={18} />
            </button>
          </div>
        );
      })}
    </div>
  );
}

// ─── Aurora Background ───────────────────────────────────
function AuroraBackground() {
  return (
    <div className="fixed inset-0 -z-10 overflow-hidden pointer-events-none">
      <div className="absolute top-[5%] right-[10%] w-72 h-72 bg-teal-500/10 rounded-full blur-[120px]" />
      <div className="absolute bottom-[10%] left-[15%] w-96 h-96 bg-emerald-500/10 rounded-full blur-[140px]" />
    </div>
  );
}

// ─── Header ──────────────────────────────────────────────
interface HeaderProps {
  settings: StoreSettings;
  onAdminClick: () => void;
  onMenuToggle: () => void;
  mobileMenuOpen: boolean;
  isCloudConnected: boolean;
}
function Header({ settings, onAdminClick, onMenuToggle, mobileMenuOpen, isCloudConnected }: HeaderProps) {
  return (
    <header className="sticky top-0 z-50 bg-zinc-950/80 backdrop-blur-md border-b border-zinc-900">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="flex items-center justify-between h-20">
          <div className="flex items-center gap-3">
            <div className="w-12 h-12 rounded-2xl bg-teal-500/10 border border-teal-500/20 p-[2px] shadow-lg">
              <div className="w-full h-full rounded-2xl bg-zinc-950 flex items-center justify-center overflow-hidden">
                {settings.logo ? (
                  <img src={settings.logo} alt="logo" className="w-full h-full object-cover" />
                ) : (
                  <Store size={24} className="text-teal-400" />
                )}
              </div>
            </div>
            <div>
              <div className="flex items-center gap-2">
                <h1 className="text-xl font-black tracking-tight text-teal-400 leading-none">{settings.storeName}</h1>
                <span className={`inline-flex items-center gap-1 px-2 py-0.5 rounded-full text-[10px] font-bold border ${isCloudConnected ? 'bg-emerald-500/20 text-emerald-400 border-emerald-500/30' : 'bg-amber-500/20 text-amber-400 border-amber-500/30'}`}>
                  <Database size={10} />
                  <span>{isCloudConnected ? 'متصل بقاعدة السحابة المجانية' : 'وضع محلي سحابي'}</span>
                </span>
              </div>
              <p className="text-[11px] text-zinc-400 mt-1 font-medium">{settings.tagline}</p>
            </div>
          </div>

          <nav className="hidden md:flex items-center gap-1">
            {getOrderedCategories(settings.categoryOrder).map((cat) => (
              <a
                key={cat.id}
                href={`#catalog`}
                className="px-4 py-2 rounded-xl text-sm text-zinc-300 hover:text-white hover:bg-zinc-900 transition font-medium"
              >
                {cat.label}
              </a>
            ))}
          </nav>

          <div className="flex items-center gap-2">
            <a
              href={settings.instagramUrl}
              target="_blank"
              rel="noopener noreferrer"
              className="hidden sm:flex items-center gap-2 px-4 py-2.5 rounded-xl bg-teal-500 hover:bg-teal-400 text-zinc-950 text-sm font-bold shadow-lg transition-all"
            >
              <Instagram size={18} />
              <span>تابعنا</span>
            </a>
            <button
              onClick={onAdminClick}
              className="w-10 h-10 rounded-xl bg-zinc-900 border border-zinc-800 flex items-center justify-center text-zinc-400 hover:text-zinc-100 hover:bg-zinc-800 transition"
              title="لوحة التحكم"
            >
              <Settings size={20} />
            </button>
            <button
              onClick={onMenuToggle}
              className="md:hidden w-10 h-10 rounded-xl bg-zinc-900 border border-zinc-800 flex items-center justify-center text-zinc-400 hover:text-zinc-100 transition"
            >
              {mobileMenuOpen ? <X size={20} /> : <Menu size={20} />}
            </button>
          </div>
        </div>

        {mobileMenuOpen && (
          <nav className="md:hidden flex flex-col gap-1 pb-4">
            {getOrderedCategories(settings.categoryOrder).map((cat) => (
              <a
                key={cat.id}
                href={`#catalog`}
                onClick={onMenuToggle}
                className="px-4 py-3 rounded-xl text-sm text-zinc-300 hover:text-white hover:bg-zinc-900 transition font-medium flex items-center gap-2"
              >
                <cat.icon size={16} />
                {cat.label}
              </a>
            ))}
          </nav>
        )}
      </div>
    </header>
  );
}

// ─── Hero Section ────────────────────────────────────────
interface HeroProps {
  settings: StoreSettings;
  onShopNow: () => void;
  productCount: number;
}
function Hero({ settings, onShopNow, productCount }: HeroProps) {
  return (
    <section className="relative pt-20 pb-24 px-4 sm:px-6 lg:px-8 overflow-hidden">
      <div className="max-w-5xl mx-auto text-center relative z-10">
        <div className="inline-flex items-center gap-2 px-5 py-2 rounded-full bg-zinc-900 border border-zinc-800 mb-8">
          <Sparkles size={16} className="text-teal-400" />
          <span className="text-sm text-zinc-300 font-medium">مجموعة فاخرة ومنتقاة بعناية</span>
        </div>

        <h2 className="text-4xl sm:text-5xl md:text-6xl lg:text-7xl font-black leading-[1.15]">
          <span className="block text-zinc-100">{settings.heroTitle1}</span>
          <span className="block text-teal-400 mt-2">{settings.heroTitle2}</span>
        </h2>

        <p className="text-zinc-400 text-lg sm:text-xl mt-7 max-w-2xl mx-auto leading-relaxed">
          اكتشف مجموعتنا الحصرية من أدوات المطبخ والمنزل الفاخرة. منتجات مختارة بعناية تمنح مساحتك أناقة ووظيفية استثنائية.
        </p>

        <div className="flex flex-col sm:flex-row items-center justify-center gap-4 mt-10">
          <button
            onClick={onShopNow}
            className="group flex items-center gap-2 px-8 py-4 rounded-2xl bg-teal-500 hover:bg-teal-400 text-zinc-950 font-black text-lg shadow-xl shadow-teal-950/60 transition-all hover:scale-105"
          >
            <ShoppingBag size={22} />
            <span>تسوق المجموعة</span>
            <ArrowLeft size={20} className="group-hover:-translate-x-1 transition-transform" />
          </button>
          <a
            href={settings.instagramUrl}
            target="_blank"
            rel="noopener noreferrer"
            className="flex items-center gap-2 px-8 py-4 rounded-2xl bg-zinc-900 hover:bg-zinc-800 border border-zinc-800 text-zinc-100 font-bold text-lg transition-all"
          >
            <Instagram size={22} />
            <span>تواصل معنا</span>
          </a>
        </div>

        <div className="grid grid-cols-2 gap-4 sm:gap-8 mt-16 max-w-lg mx-auto">
          {[
            { value: `${productCount}`, label: 'منتج فاخر' },
            { value: '4.9★', label: 'تقييم العملاء' },
          ].map((stat, i) => (
            <div key={i} className="bg-zinc-900/60 rounded-2xl py-5 px-3 border border-zinc-800">
              <div className="text-2xl sm:text-3xl font-black text-teal-400">{stat.value}</div>
              <div className="text-xs sm:text-sm text-zinc-400 mt-1 font-medium">{stat.label}</div>
            </div>
          ))}
        </div>
      </div>
    </section>
  );
}

// ─── Image Upload Component ──────────────────────────────
interface ImageUploaderProps {
  label: string;
  currentValue: string;
  onChange: (value: string) => void;
  maxSize?: number;
}

function ImageUploader({ label, currentValue, onChange, maxSize = 600 }: ImageUploaderProps) {
  const [tab, setTab] = useState<'upload' | 'url'>('upload');
  const [loading, setLoading] = useState(false);
  const fileInputRef = useRef<HTMLInputElement>(null);

  const handleFileChange = async (e: React.ChangeEvent<HTMLInputElement>) => {
    const file = e.target.files?.[0];
    if (!file) return;
    setLoading(true);
    try {
      const base64 = await compressImage(file, maxSize);
      onChange(base64);
    } catch (err) {
      console.error('Error uploading image:', err);
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="space-y-2">
      <label className="block text-sm font-medium text-white/80">{label}</label>
      
      <div className="flex gap-2 p-1 bg-white/5 rounded-xl border border-white/10 w-fit text-xs font-medium">
        <button
          type="button"
          onClick={() => setTab('upload')}
          className={`flex items-center gap-1.5 px-3 py-1.5 rounded-lg transition ${
            tab === 'upload' ? 'bg-teal-500 text-white font-bold' : 'text-white/60 hover:text-white'
          }`}
        >
          <FileImage size={14} />
          <span>رفع صورة من الجهاز</span>
        </button>
        <button
          type="button"
          onClick={() => setTab('url')}
          className={`flex items-center gap-1.5 px-3 py-1.5 rounded-lg transition ${
            tab === 'url' ? 'bg-teal-500 text-white font-bold' : 'text-white/60 hover:text-white'
          }`}
        >
          <LinkIcon size={14} />
          <span>رابط صورة</span>
        </button>
      </div>

      {tab === 'upload' ? (
        <div className="flex items-center gap-3">
          <input
            type="file"
            ref={fileInputRef}
            onChange={handleFileChange}
            accept="image/*"
            className="hidden"
          />
          <button
            type="button"
            onClick={() => fileInputRef.current?.click()}
            disabled={loading}
            className="flex items-center gap-2 px-4 py-3 rounded-xl glass hover:bg-white/10 transition text-sm text-white/90 font-medium border border-white/10"
          >
            {loading ? <Loader2 size={18} className="animate-spin text-teal-300" /> : <Upload size={18} className="text-teal-300" />}
            <span>{loading ? 'جاري رفع الصورة...' : 'اختر صورة من جهازك'}</span>
          </button>

          {currentValue && (
            <div className="relative w-12 h-12 rounded-xl overflow-hidden border border-white/20 shrink-0">
              <img src={currentValue} alt="Preview" className="w-full h-full object-cover" />
              <button
                type="button"
                onClick={() => onChange('')}
                className="absolute inset-0 bg-black/60 flex items-center justify-center text-white opacity-0 hover:opacity-100 transition"
              >
                <X size={16} />
              </button>
            </div>
          )}
        </div>
      ) : (
        <input
          type="text"
          value={currentValue}
          onChange={(e) => onChange(e.target.value)}
          placeholder="https://example.com/image.jpg"
          className="w-full px-4 py-3 rounded-xl bg-white/5 border border-white/10 text-white placeholder:text-white/30 text-sm focus:outline-none focus:border-teal-400"
        />
      )}
    </div>
  );
}

// ─── Star Rating Component ───────────────────────────────
function StarRating({ value, onChange, size = 26 }: { value: number; onChange?: (v: number) => void; size?: number }) {
  const [hover, setHover] = useState(0);
  const display = hover || value;
  return (
    <div className="flex items-center gap-1" dir="ltr">
      {[1, 2, 3, 4, 5].map((star) => (
        <button
          key={star}
          type="button"
          disabled={!onChange}
          onClick={() => onChange?.(star)}
          onMouseEnter={() => onChange && setHover(star)}
          onMouseLeave={() => onChange && setHover(0)}
          className={`transition-all duration-200 ${onChange ? 'hover:scale-125 cursor-pointer' : 'cursor-default'}`}
        >
          <Star
            size={size}
            className={star <= display ? 'fill-teal-400 text-teal-400 drop-shadow-[0_0_8px_rgba(45,212,191,0.5)]' : 'text-zinc-700'}
          />
        </button>
      ))}
    </div>
  );
}

// ─── Product Card ────────────────────────────────────────
interface ProductCardProps {
  product: Product;
  onOrder: (product: Product) => void;
  onView: (product: Product) => void;
  index: number;
}
function ProductCard({ product, onOrder, onView, index }: ProductCardProps) {
  return (
    <div className="group bg-zinc-900/90 hover:bg-zinc-900 rounded-3xl overflow-hidden transition-all duration-300 hover:-translate-y-2 hover:shadow-2xl hover:shadow-black/80 border border-zinc-800/90 hover:border-teal-500/40 flex flex-col justify-between">
      <div>
        <div className="p-2.5">
          <div 
            className="relative aspect-square rounded-2xl overflow-hidden cursor-pointer bg-zinc-950 flex items-center justify-center border border-teal-500/30 group-hover:border-teal-400/60 shadow-[0_0_15px_rgba(45,212,191,0.12)] transition-all duration-500" 
            onClick={() => onView(product)}
          >
            <img
              src={product.image || DEFAULT_PRODUCT_IMAGE}
              alt={product.name}
              loading="lazy"
              onError={(e) => {
                (e.target as HTMLImageElement).src = DEFAULT_PRODUCT_IMAGE;
              }}
              className="w-full h-full object-cover group-hover:scale-108 transition-transform duration-700 opacity-90 group-hover:opacity-100"
            />
            <div className="absolute inset-0 bg-gradient-to-t from-zinc-950/80 via-transparent to-transparent opacity-60 group-hover:opacity-40 transition-opacity" />

            {product.oldPrice && parseFloat(product.oldPrice) > 0 && parseFloat(product.price) > 0 && (
              <div className="absolute top-3 left-3 px-2.5 py-1 rounded-full bg-rose-500/20 text-rose-400 border border-rose-500/30 text-xs font-black shadow-lg backdrop-blur-md">
                {Math.round((1 - parseFloat(product.price) / parseFloat(product.oldPrice)) * 100)}%-
              </div>
            )}

            <div className="absolute bottom-3 left-1/2 -translate-x-1/2 opacity-0 group-hover:opacity-100 transition-all duration-300 group-hover:bottom-4">
              <div className="bg-zinc-950/90 rounded-full px-4 py-2 flex items-center gap-2 text-zinc-200 text-xs font-bold border border-teal-500/40 shadow-xl backdrop-blur-md">
                <Eye size={15} className="text-teal-400" />
                <span>عرض التفاصيل</span>
              </div>
            </div>
          </div>
        </div>

        <div className="p-5 pt-1 flex flex-col">
          <h3 className="font-bold text-zinc-100 text-base leading-snug mb-2.5 line-clamp-2 min-h-[2.8em]">{product.name}</h3>

          {product.pieceCount != null && product.pieceCount > 0 && (
            <div className="mb-3">
              <span className="inline-flex items-center gap-1.5 px-2.5 py-1 rounded-lg bg-teal-500/10 text-teal-300 text-xs font-extrabold border border-teal-500/20">
                <Package size={13} />
                <span>{product.pieceCount} {product.pieceCount === 1 ? 'قطعة' : 'قطع'}</span>
              </span>
            </div>
          )}

          {(() => {
            const dims = getFilledDimensions(product.dimensions);
            if (dims.length === 0) return <div className="min-h-[2em] mb-4" />;
            return (
              <div className="flex flex-wrap gap-1.5 mb-4 min-h-[2em]">
                {dims.map((d) => (
                  <span key={d.label} className="inline-flex items-center gap-1 px-2 py-0.5 rounded-lg bg-zinc-950 text-[11px] text-zinc-400 font-medium border border-zinc-800">
                    <span className="text-teal-400 font-bold">{d.label}</span>
                    <span className="text-zinc-200 font-bold">{d.value} سم</span>
                  </span>
                ))}
              </div>
            );
          })()}

          <div className="flex items-center justify-between gap-2 mb-4 mt-auto">
            <div className="flex flex-col gap-0.5">
              <div className="flex items-baseline gap-1.5">
                <span className="text-2xl sm:text-3xl font-black tracking-tight text-teal-400">{product.price}</span>
                <span className="text-xs text-zinc-500 font-bold">د.ع</span>
              </div>
              {product.oldPrice && (
                <span className="text-xs text-zinc-600 line-through font-semibold">{product.oldPrice} د.ع</span>
              )}
            </div>

            {(() => {
              const badgeInfo = getBadgeStyle(product.badge);
              if (!badgeInfo) return null;
              return (
                <div className={`px-3 py-1 rounded-full ${badgeInfo.className} text-xs font-extrabold shadow-md shrink-0`}>
                  {badgeInfo.label}
                </div>
              );
            })()}
          </div>
        </div>
      </div>

      <div className="p-5 pt-0">
        <button
          onClick={() => onOrder(product)}
          className="w-full flex items-center justify-center gap-2 py-3.5 rounded-xl bg-zinc-800 hover:bg-teal-500 text-zinc-200 hover:text-zinc-950 border border-zinc-700/60 hover:border-teal-400 font-black text-sm transition-all duration-200 shadow-lg active:scale-95"
        >
          <Instagram size={18} />
          <span>اطلب الآن</span>
        </button>
      </div>
    </div>
  );
}

// ─── Product Detail Modal ────────────────────────────────
interface ProductDetailModalProps {
  product: Product | null;
  settings: StoreSettings;
  onClose: () => void;
  onOrder: (product: Product) => void;
  ratings: Record<string, { avg: number; count: number }>;
  userRating: number;
  onRate: (productId: string, stars: number) => void;
}
function ProductDetailModal({ product, settings, onClose, onOrder, ratings, userRating, onRate }: ProductDetailModalProps) {
  if (!product) return null;
  const catLabel = getOrderedCategories(settings.categoryOrder).find((c) => c.id === product.category)?.label || product.category;
  const rating = ratings[product.id];
  const avg = rating?.avg ?? 0;
  const count = rating?.count ?? 0;
  return (
    <div className="fixed inset-0 z-[80] flex items-center justify-center p-4 animate-fade-in" onClick={onClose}>
      <div className="absolute inset-0 bg-black/85 backdrop-blur-md" />
      <div className="bg-zinc-900/95 rounded-3xl max-w-3xl w-full max-h-[90vh] overflow-y-auto scrollbar-thin relative border border-zinc-800 shadow-2xl shadow-black" onClick={(e) => e.stopPropagation()}>
        <button onClick={onClose} className="absolute top-4 left-4 z-10 w-10 h-10 rounded-xl bg-zinc-800 hover:bg-zinc-700 flex items-center justify-center text-zinc-400 hover:text-white transition border border-zinc-700/50">
          <X size={20} />
        </button>
        <div className="grid md:grid-cols-2 gap-0">
          <div className="p-3 md:p-4">
            <div className="relative aspect-square md:aspect-auto md:h-full overflow-hidden rounded-2xl bg-zinc-950 flex items-center justify-center border-2 border-teal-500/40 shadow-[0_0_25px_rgba(45,212,191,0.2)]">
              <img 
                src={product.image || DEFAULT_PRODUCT_IMAGE} 
                alt={product.name} 
                onError={(e) => {
                  (e.target as HTMLImageElement).src = DEFAULT_PRODUCT_IMAGE;
                }}
                className="w-full h-full object-cover" 
              />
            </div>
          </div>
          <div className="p-6 md:p-8 flex flex-col justify-between bg-zinc-900/50">
            <div>
              <div className="flex flex-wrap items-center gap-2 mb-3">
                <span className="px-3 py-1 rounded-full bg-zinc-800 text-xs text-zinc-300 font-semibold border border-zinc-700/50">{catLabel}</span>
                {product.pieceCount != null && product.pieceCount > 0 && (
                  <span className="px-3 py-1 rounded-full bg-teal-500/10 text-teal-300 text-xs font-black border border-teal-500/20 flex items-center gap-1">
                    <Package size={13} />
                    <span>{product.pieceCount} قطعة</span>
                  </span>
                )}
                {product.featured && (
                  <span className="px-3 py-1 rounded-full bg-amber-500/10 text-amber-400 text-xs font-bold flex items-center gap-1 border border-amber-500/20">
                    <Star size={12} className="fill-amber-400" />
                    مميز
                  </span>
                )}
              </div>
              <h3 className="text-2xl font-black text-zinc-100 mb-3 leading-snug">{product.name}</h3>

              <div className="mb-5 flex items-center justify-between gap-3 bg-zinc-950/80 p-3.5 rounded-2xl border border-zinc-800">
                <div className="flex items-baseline gap-2">
                  <span className="text-3xl font-black text-teal-400 tracking-tight">{product.price}</span>
                  <span className="text-sm text-zinc-500 font-bold">د.ع</span>
                  {product.oldPrice && (
                    <span className="text-sm text-zinc-600 line-through font-semibold mr-2">{product.oldPrice} د.ع</span>
                  )}
                </div>

                {(() => {
                  const badgeInfo = getBadgeStyle(product.badge);
                  if (!badgeInfo) return null;
                  return (
                    <div className={`px-3.5 py-1.5 rounded-full ${badgeInfo.className} text-xs font-extrabold shadow-md`}>
                      {badgeInfo.label}
                    </div>
                  );
                })()}
              </div>

              <div className="flex items-center gap-3 mb-4 bg-zinc-950/60 p-3 rounded-2xl border border-zinc-800/80">
                <StarRating value={Math.round(avg)} size={20} />
                <span className="text-teal-400 font-black text-sm">
                  {count > 0 ? `${avg.toFixed(1)} / 5` : 'لا تقييمات بعد'}
                </span>
                {count > 0 && (
                  <span className="text-zinc-500 text-xs font-bold">({count} تقييم)</span>
                )}
              </div>

              {product.description && (
                <div className="mb-5 bg-zinc-950/60 rounded-2xl p-4 border border-zinc-800/80">
                  <h4 className="text-xs font-black text-teal-400 mb-1.5 flex items-center gap-1.5">
                    <Info size={14} />
                    <span>تفاصيل المنتج:</span>
                  </h4>
                  <p className="text-zinc-300 text-sm leading-relaxed whitespace-pre-line font-medium">
                    {product.description}
                  </p>
                </div>
              )}

              <div className="mb-6">
                {(() => {
                  const dims = getFilledDimensions(product.dimensions);
                  if (dims.length === 0) {
                    return null;
                  }
                  return (
                    <div className="space-y-2">
                      <span className="text-zinc-400 text-xs font-bold uppercase tracking-wider">أبعاد وقياسات المنتج:</span>
                      <div className="grid grid-cols-2 gap-2.5">
                        {dims.map((d) => (
                          <div key={d.label} className="bg-zinc-950 rounded-xl px-3.5 py-2.5 flex items-center justify-between border border-zinc-800">
                            <span className="text-zinc-400 text-xs font-bold">{d.label}</span>
                            <span className="text-teal-400 font-black text-sm">{d.value} <span className="text-xs text-teal-500 font-semibold">سم</span></span>
                          </div>
                        ))}
                      </div>
                    </div>
                  );
                })()}
              </div>
            </div>

            <div>
              <div className="mb-5 bg-zinc-950 rounded-2xl p-4 border border-zinc-800 text-center sm:text-right">
                <p className="text-zinc-300 text-xs font-extrabold mb-2">قيّم هذا المنتج (5 نجمات تركوازية):</p>
                <div className="flex items-center justify-between flex-wrap gap-2">
                  <StarRating value={userRating} onChange={(v) => onRate(product.id, v)} size={28} />
                  {userRating > 0 && (
                    <span className="text-teal-400 text-xs font-bold animate-fade-in bg-teal-500/10 px-3 py-1 rounded-full border border-teal-500/20">
                      تم التقييم بـ {userRating} من 5 ✨
                    </span>
                  )}
                </div>
              </div>

              <button
                onClick={() => onOrder(product)}
                className="w-full flex items-center justify-center gap-3 py-4 rounded-2xl bg-teal-500 hover:bg-teal-400 text-zinc-950 font-black text-base shadow-xl shadow-teal-950/60 transition-all hover:scale-[1.02] active:scale-95"
              >
                <Instagram size={20} />
                <span>اطلب الآن عبر انستغرام</span>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}

// ─── Admin Panel Modal ───────────────────────────────────
interface AdminPanelProps {
  open: boolean;
  onClose: () => void;
  products: Product[];
  onSaveProducts: (products: Product[]) => void;
  settings: StoreSettings;
  onSaveSettings: (settings: StoreSettings) => void;
  addToast: (type: ToastType, msg: string) => void;
}

function AdminPanel({ open, onClose, products, onSaveProducts, settings, onSaveSettings, addToast }: AdminPanelProps) {
  const [isAuthenticated, setIsAuthenticated] = useState(false);
  const [passwordInput, setPasswordInput] = useState('');
  const [newPasswordInput, setNewPasswordInput] = useState('');
  const [activeTab, setActiveTab] = useState<'products' | 'settings' | 'security'>('products');
  const [editingProduct, setEditingProduct] = useState<Product | null>(null);
  const [showAddForm, setShowAddForm] = useState(false);

  const [prodForm, setProdForm] = useState<Partial<Product>>({
    name: '',
    description: '',
    price: '',
    oldPrice: '',
    category: 'cookware',
    image: '',
    badge: 'none',
    featured: false,
    pieceCount: undefined,
    dimensions: { length: undefined, width: undefined, height: undefined, diameter: undefined },
  });

  const [tempSettings, setTempSettings] = useState<StoreSettings>(settings);

  useEffect(() => {
    setTempSettings(settings);
  }, [settings]);

  useEffect(() => {
    if (!open) {
      setIsAuthenticated(false);
      setPasswordInput('');
    }
  }, [open]);

  if (!open) return null;

  const handleLogin = (e: React.FormEvent) => {
    e.preventDefault();
    const correctPassword = getAdminPassword();
    if (passwordInput === correctPassword) {
      setIsAuthenticated(true);
      addToast('success', 'تم تسجيل الدخول بنجاح');
    } else {
      addToast('error', 'كلمة المرور غير صحيحة');
    }
  };

  const handleSaveProduct = async (e: React.FormEvent) => {
    e.preventDefault();
    if (!prodForm.name || !prodForm.price || !prodForm.image) {
      addToast('warning', 'يرجى ملء الاسم، السعر والصورة كحد أدنى');
      return;
    }

    let updatedProducts = [...products];
    if (editingProduct) {
      updatedProducts = products.map((p) => p.id === editingProduct.id ? { ...p, ...prodForm } as Product : p);
      addToast('success', 'تم تعديل المنتج بنجاح');
    } else {
      const newProd: Product = {
        id: generateId(),
        name: prodForm.name || '',
        description: prodForm.description || '',
        price: prodForm.price || '0',
        oldPrice: prodForm.oldPrice || '',
        category: prodForm.category || 'cookware',
        image: prodForm.image || '',
        badge: prodForm.badge || 'none',
        featured: !!prodForm.featured,
        pieceCount: prodForm.pieceCount ? Number(prodForm.pieceCount) : undefined,
        dimensions: prodForm.dimensions || {},
      };
      updatedProducts = [newProd, ...products];
      addToast('success', 'تمت إضافة المنتج بنجاح');
    }

    onSaveProducts(updatedProducts);
    setEditingProduct(null);
    setShowAddForm(false);
    setProdForm({
      name: '',
      description: '',
      price: '',
      oldPrice: '',
      category: 'cookware',
      image: '',
      badge: 'none',
      featured: false,
      pieceCount: undefined,
      dimensions: {},
    });
  };

  const handleDeleteProduct = (id: string) => {
    const updated = products.filter((p) => p.id !== id);
    onSaveProducts(updated);
    addToast('success', 'تم حذف المنتج');
  };

  const handleSaveSettingsSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    onSaveSettings(tempSettings);
    addToast('success', 'تم حفظ إعدادات المتجر بنجاح');
  };

  const handlePasswordChange = (e: React.FormEvent) => {
    e.preventDefault();
    if (!newPasswordInput || newPasswordInput.length < 4) {
      addToast('warning', 'يجب أن تكون كلمة المرور 4 أحرف على الأقل');
      return;
    }
    try {
      localStorage.setItem(STORAGE_KEYS.adminPassword, newPasswordInput);
      addToast('success', 'تم تحديث كلمة المرور بنجاح');
      setNewPasswordInput('');
    } catch {
      addToast('error', 'حدث خطأ أثناء حفظ كلمة المرور');
    }
  };

  return (
    <div className="fixed inset-0 z-[90] flex items-center justify-center p-4 animate-fade-in">
      <div className="absolute inset-0 bg-black/85 backdrop-blur-md" onClick={onClose} />
      <div className="bg-zinc-900/95 rounded-3xl max-w-4xl w-full max-h-[90vh] overflow-y-auto p-6 sm:p-8 relative z-10 border border-zinc-800 shadow-2xl shadow-black" onClick={(e) => e.stopPropagation()}>
        <button onClick={onClose} className="absolute top-6 left-6 text-zinc-500 hover:text-white transition">
          <X size={24} />
        </button>

        {!isAuthenticated ? (
          <div className="max-w-md mx-auto py-12 text-center">
            <div className="w-16 h-16 rounded-2xl bg-teal-500/10 border border-teal-500/20 flex items-center justify-center mx-auto mb-5 text-teal-400">
              <Lock size={30} />
            </div>
            <h3 className="text-2xl font-black text-zinc-100 mb-2">لوحة التحكم المحمية</h3>
            <p className="text-zinc-400 text-sm mb-6">يرجى إدخال كلمة المرور للوصول إلى لوحة تحكم المتجر (الافتراضية: glow2024)</p>
            <form onSubmit={handleLogin} className="space-y-4">
              <input
                type="password"
                value={passwordInput}
                onChange={(e) => setPasswordInput(e.target.value)}
                placeholder="كلمة المرور..."
                className="w-full px-4 py-3.5 rounded-2xl bg-zinc-950 border border-zinc-800 text-zinc-100 text-center tracking-widest focus:outline-none focus:border-teal-500 text-lg"
                autoFocus
              />
              <button
                type="submit"
                className="w-full py-4 rounded-2xl bg-teal-500 hover:bg-teal-400 text-zinc-950 font-black text-base shadow-lg shadow-teal-950/50 transition"
              >
                دخول لوحة التحكم
              </button>
            </form>
          </div>
        ) : (
          <div>
            <div className="flex flex-wrap items-center justify-between border-b border-zinc-800 pb-6 mb-6 gap-4">
              <div>
                <h3 className="text-2xl font-bold text-zinc-100">إدارة المتجر السحابي</h3>
                <div className="flex items-center gap-2 mt-1 text-xs text-zinc-400">
                  <Database size={14} className="text-emerald-400" />
                  <span>تخزين سحابي مجاني ومباشر</span>
                </div>
              </div>
              <div className="flex flex-wrap gap-2 bg-zinc-950 p-1.5 rounded-2xl border border-zinc-800">
                <button
                  onClick={() => setActiveTab('products')}
                  className={`px-4 py-2 rounded-xl font-bold text-sm transition ${activeTab === 'products' ? 'bg-teal-500 text-zinc-950' : 'text-zinc-400 hover:text-zinc-100'}`}
                >
                  المنتجات ({products.length})
                </button>
                <button
                  onClick={() => setActiveTab('settings')}
                  className={`px-4 py-2 rounded-xl font-bold text-sm transition ${activeTab === 'settings' ? 'bg-teal-500 text-zinc-950' : 'text-zinc-400 hover:text-zinc-100'}`}
                >
                  إعدادات المتجر
                </button>
                <button
                  onClick={() => setActiveTab('security')}
                  className={`px-4 py-2 rounded-xl font-bold text-sm transition ${activeTab === 'security' ? 'bg-teal-500 text-zinc-950' : 'text-zinc-400 hover:text-zinc-100'}`}
                >
                  كلمة المرور
                </button>
              </div>
            </div>

            {/* TAB 1: PRODUCTS */}
            {activeTab === 'products' && (
              <div>
                {!showAddForm && !editingProduct ? (
                  <div>
                    <button
                      onClick={() => {
                        setEditingProduct(null);
                        setProdForm({
                          name: '',
                          description: '',
                          price: '',
                          oldPrice: '',
                          category: 'cookware',
                          image: '',
                          badge: 'none',
                          featured: false,
                          pieceCount: undefined,
                          dimensions: { length: undefined, width: undefined, height: undefined, diameter: undefined },
                        });
                        setShowAddForm(true);
                      }}
                      className="w-full py-4 rounded-2xl border-2 border-dashed border-zinc-800 hover:border-teal-500 text-zinc-400 hover:text-teal-400 transition flex items-center justify-center gap-2 font-bold mb-6 bg-zinc-950/40"
                    >
                      <Plus size={20} />
                      <span>إضافة منتج جديد</span>
                    </button>

                    <div className="grid gap-4">
                      {products.map((p) => (
                        <div key={p.id} className="bg-zinc-950/80 rounded-2xl p-4 flex items-center justify-between gap-4 border border-zinc-800">
                          <img src={p.image || DEFAULT_PRODUCT_IMAGE} alt={p.name} className="w-16 h-16 rounded-xl object-cover shrink-0 bg-zinc-900" />
                          <div className="flex-1 min-w-0">
                            <h4 className="text-zinc-100 font-bold truncate">{p.name}</h4>
                            <div className="flex items-center gap-3 text-xs mt-1">
                              <span className="text-teal-400 font-bold">{formatPrice(p.price)}</span>
                              {p.pieceCount != null && (
                                <span className="text-zinc-500">({p.pieceCount} قطع)</span>
                              )}
                            </div>
                          </div>
                          <div className="flex items-center gap-2">
                            <button
                              onClick={() => {
                                setEditingProduct(p);
                                setProdForm(p);
                                setShowAddForm(true);
                              }}
                              className="w-10 h-10 rounded-xl bg-zinc-800 hover:bg-zinc-700 text-zinc-300 flex items-center justify-center transition border border-zinc-700/50"
                            >
                              <Edit2 size={18} />
                            </button>
                            <button
                              onClick={() => handleDeleteProduct(p.id)}
                              className="w-10 h-10 rounded-xl bg-rose-500/10 hover:bg-rose-500/20 text-rose-400 flex items-center justify-center transition border border-rose-500/20"
                            >
                              <Trash2 size={18} />
                            </button>
                          </div>
                        </div>
                      ))}
                    </div>
                  </div>
                ) : (
                  <form onSubmit={handleSaveProduct} className="space-y-4">
                    <h4 className="text-lg font-bold text-zinc-100 mb-4">{editingProduct ? 'تعديل المنتج' : 'إضافة منتج جديد'}</h4>

                    <ImageUploader
                      label="صورة المنتج"
                      currentValue={prodForm.image || ''}
                      onChange={(val) => setProdForm({ ...prodForm, image: val })}
                      maxSize={800}
                    />

                    <div>
                      <label className="block text-sm text-zinc-400 mb-1">عنوان / اسم المنتج</label>
                      <input
                        type="text"
                        value={prodForm.name || ''}
                        onChange={(e) => setProdForm({ ...prodForm, name: e.target.value })}
                        placeholder="مثال: طقم أواني ستانلس ستيل فاخر"
                        className="w-full px-4 py-3 rounded-xl bg-zinc-950 border border-zinc-800 text-zinc-100 focus:outline-none focus:border-teal-500"
                        required
                      />
                    </div>

                    <div>
                      <label className="block text-sm text-zinc-400 mb-1">تفاصيل ووصف المنتج</label>
                      <textarea
                        rows={3}
                        value={prodForm.description || ''}
                        onChange={(e) => setProdForm({ ...prodForm, description: e.target.value })}
                        placeholder="أدخل مواصفات المنتج، المواد، تعليمات الاستخدام..."
                        className="w-full px-4 py-3 rounded-xl bg-zinc-950 border border-zinc-800 text-zinc-100 placeholder:text-zinc-600 focus:outline-none focus:border-teal-500 text-sm"
                      />
                    </div>

                    <div className="bg-zinc-950 p-4 rounded-2xl border border-zinc-800 space-y-3">
                      <h5 className="text-xs font-bold text-teal-400 uppercase tracking-wider">قياسات المنتج وعدد القطع</h5>
                      <div className="grid grid-cols-2 sm:grid-cols-5 gap-3">
                        <div>
                          <label className="block text-xs text-zinc-400 mb-1">الارتفاع (سم)</label>
                          <input
                            type="number"
                            value={prodForm.dimensions?.height ?? ''}
                            onChange={(e) => setProdForm({
                              ...prodForm,
                              dimensions: { ...prodForm.dimensions, height: e.target.value ? Number(e.target.value) : undefined }
                            })}
                            className="w-full px-3 py-2.5 rounded-xl bg-zinc-900 border border-zinc-800 text-zinc-100 text-sm focus:outline-none focus:border-teal-500"
                          />
                        </div>
                        <div>
                          <label className="block text-xs text-zinc-400 mb-1">الطول (سم)</label>
                          <input
                            type="number"
                            value={prodForm.dimensions?.length ?? ''}
                            onChange={(e) => setProdForm({
                              ...prodForm,
                              dimensions: { ...prodForm.dimensions, length: e.target.value ? Number(e.target.value) : undefined }
                            })}
                            className="w-full px-3 py-2.5 rounded-xl bg-zinc-900 border border-zinc-800 text-zinc-100 text-sm focus:outline-none focus:border-teal-500"
                          />
                        </div>
                        <div>
                          <label className="block text-xs text-zinc-400 mb-1">العرض (سم)</label>
                          <input
                            type="number"
                            value={prodForm.dimensions?.width ?? ''}
                            onChange={(e) => setProdForm({
                              ...prodForm,
                              dimensions: { ...prodForm.dimensions, width: e.target.value ? Number(e.target.value) : undefined }
                            })}
                            className="w-full px-3 py-2.5 rounded-xl bg-zinc-900 border border-zinc-800 text-zinc-100 text-sm focus:outline-none focus:border-teal-500"
                          />
                        </div>
                        <div>
                          <label className="block text-xs text-zinc-400 mb-1">القطر (سم)</label>
                          <input
                            type="number"
                            value={prodForm.dimensions?.diameter ?? ''}
                            onChange={(e) => setProdForm({
                              ...prodForm,
                              dimensions: { ...prodForm.dimensions, diameter: e.target.value ? Number(e.target.value) : undefined }
                            })}
                            className="w-full px-3 py-2.5 rounded-xl bg-zinc-900 border border-zinc-800 text-zinc-100 text-sm focus:outline-none focus:border-teal-500"
                          />
                        </div>
                        <div className="col-span-2 sm:col-span-1">
                          <label className="block text-xs text-teal-400 font-bold mb-1">عدد القطع</label>
                          <input
                            type="number"
                            value={prodForm.pieceCount ?? ''}
                            onChange={(e) => setProdForm({ ...prodForm, pieceCount: e.target.value ? Number(e.target.value) : undefined })}
                            placeholder="مثال: 12"
                            className="w-full px-3 py-2.5 rounded-xl bg-zinc-900 border border-teal-500/40 text-zinc-100 text-sm focus:outline-none focus:border-teal-400"
                          />
                        </div>
                      </div>
                    </div>

                    <div className="grid grid-cols-1 sm:grid-cols-3 gap-4">
                      <div>
                        <label className="block text-sm text-zinc-400 mb-1">السعر الحالي (د.ع)</label>
                        <input
                          type="text"
                          value={prodForm.price || ''}
                          onChange={(e) => setProdForm({ ...prodForm, price: e.target.value })}
                          placeholder="250"
                          className="w-full px-4 py-3 rounded-xl bg-zinc-950 border border-zinc-800 text-zinc-100 focus:outline-none focus:border-teal-500"
                          required
                        />
                      </div>
                      <div>
                        <label className="block text-sm text-zinc-400 mb-1">السعر السابق (اختياري)</label>
                        <input
                          type="text"
                          value={prodForm.oldPrice || ''}
                          onChange={(e) => setProdForm({ ...prodForm, oldPrice: e.target.value })}
                          placeholder="300"
                          className="w-full px-4 py-3 rounded-xl bg-zinc-950 border border-zinc-800 text-zinc-100 focus:outline-none focus:border-teal-500"
                        />
                      </div>
                      <div>
                        <label className="block text-sm text-zinc-400 mb-1">التصنيف</label>
                        <select
                          value={prodForm.category || 'cookware'}
                          onChange={(e) => setProdForm({ ...prodForm, category: e.target.value })}
                          className="w-full px-4 py-3 rounded-xl bg-zinc-950 border border-zinc-800 text-zinc-100 focus:outline-none focus:border-teal-500"
                        >
                          {ALL_CATEGORIES.filter((c) => c.id !== 'all').map((c) => (
                            <option key={c.id} value={c.id}>{c.label}</option>
                          ))}
                        </select>
                      </div>
                    </div>

                    <div className="grid grid-cols-2 gap-4">
                      <div>
                        <label className="block text-sm text-zinc-400 mb-1">الشارة (Badge)</label>
                        <select
                          value={prodForm.badge || 'none'}
                          onChange={(e) => setProdForm({ ...prodForm, badge: e.target.value as BadgeType })}
                          className="w-full px-4 py-3 rounded-xl bg-zinc-950 border border-zinc-800 text-zinc-100 focus:outline-none focus:border-teal-500"
                        >
                          {BADGE_OPTIONS.map((b) => (
                            <option key={b.value} value={b.value}>{b.label}</option>
                          ))}
                        </select>
                      </div>
                      <div className="flex items-center gap-3 pt-6">
                        <input
                          type="checkbox"
                          id="feat"
                          checked={!!prodForm.featured}
                          onChange={(e) => setProdForm({ ...prodForm, featured: e.target.checked })}
                          className="w-5 h-5 accent-teal-500 rounded cursor-pointer"
                        />
                        <label htmlFor="feat" className="text-zinc-200 text-sm cursor-pointer font-bold">منتج مميز</label>
                      </div>
                    </div>

                    <div className="flex gap-3 pt-4">
                      <button
                        type="button"
                        onClick={() => { setShowAddForm(false); setEditingProduct(null); }}
                        className="flex-1 py-3 rounded-xl bg-zinc-800 text-zinc-300 hover:text-white"
                      >
                        إلغاء
                      </button>
                      <button
                        type="submit"
                        className="flex-1 py-3 rounded-xl bg-teal-500 text-zinc-950 font-black hover:bg-teal-400 transition"
                      >
                        حفظ المنتج
                      </button>
                    </div>
                  </form>
                )}
              </div>
            )}

            {/* TAB 2: SETTINGS */}
            {activeTab === 'settings' && (
              <form onSubmit={handleSaveSettingsSubmit} className="space-y-4">
                <div>
                  <label className="block text-sm text-zinc-400 mb-2">اسم المتجر</label>
                  <input
                    type="text"
                    value={tempSettings.storeName}
                    onChange={(e) => setTempSettings({ ...tempSettings, storeName: e.target.value })}
                    className="w-full px-4 py-3 rounded-xl bg-zinc-950 border border-zinc-800 text-zinc-100 focus:outline-none focus:border-teal-500"
                  />
                </div>
                <div>
                  <label className="block text-sm text-zinc-400 mb-2">الوصف المختصر (Tagline)</label>
                  <input
                    type="text"
                    value={tempSettings.tagline}
                    onChange={(e) => setTempSettings({ ...tempSettings, tagline: e.target.value })}
                    className="w-full px-4 py-3 rounded-xl bg-zinc-950 border border-zinc-800 text-zinc-100 focus:outline-none focus:border-teal-500"
                  />
                </div>
                <div>
                  <label className="block text-sm text-zinc-400 mb-2">رابط حساب انستغرام</label>
                  <input
                    type="text"
                    value={tempSettings.instagramUrl}
                    onChange={(e) => setTempSettings({ ...tempSettings, instagramUrl: e.target.value })}
                    className="w-full px-4 py-3 rounded-xl bg-zinc-950 border border-zinc-800 text-zinc-100 focus:outline-none focus:border-teal-500"
                  />
                </div>

                <ImageUploader
                  label="شعار المتجر (اللوجو)"
                  currentValue={tempSettings.logo || ''}
                  onChange={(val) => setTempSettings({ ...tempSettings, logo: val })}
                  maxSize={300}
                />

                <button
                  type="submit"
                  className="w-full py-4 rounded-xl bg-teal-500 text-zinc-950 font-black hover:bg-teal-400 transition mt-6"
                >
                  حفظ إعدادات المتجر
                </button>
              </form>
            )}

            {/* TAB 3: SECURITY */}
            {activeTab === 'security' && (
              <form onSubmit={handlePasswordChange} className="space-y-4 max-w-md mx-auto py-4">
                <h4 className="text-lg font-bold text-zinc-100 mb-2">تغيير كلمة مرور لوحة التحكم</h4>
                <p className="text-zinc-400 text-xs mb-4">أدخل كلمة المرور الجديدة لحماية لوحة التحكم الخاصة بك.</p>
                <div>
                  <label className="block text-sm text-zinc-400 mb-2">كلمة المرور الجديدة</label>
                  <input
                    type="password"
                    value={newPasswordInput}
                    onChange={(e) => setNewPasswordInput(e.target.value)}
                    placeholder="أدخل كلمة المرور الجديدة..."
                    className="w-full px-4 py-3 rounded-xl bg-zinc-950 border border-zinc-800 text-zinc-100 focus:outline-none focus:border-teal-500"
                    required
                  />
                </div>
                <button
                  type="submit"
                  className="w-full py-4 rounded-xl bg-teal-500 text-zinc-950 font-black hover:bg-teal-400 transition mt-4"
                >
                  تحديث كلمة المرور
                </button>
              </form>
            )}
          </div>
        )}
      </div>
    </div>
  );
}

// ─── Main App Component ──────────────────────────────────
export default function App() {
  const [products, setProducts] = useState<Product[]>(DEFAULT_PRODUCTS);
  const [settings, setSettings] = useState<StoreSettings>(DEFAULT_SETTINGS);
  const [isCloudConnected, setIsCloudConnected] = useState(true);

  const [ratings, setRatings] = useState<Record<string, { avg: number; count: number }>>({});
  const [userRatings, setUserRatings] = useState<Record<string, number>>({});

  const [selectedCategory, setSelectedCategory] = useState<string>('all');
  const [searchQuery, setSearchQuery] = useState('');
  const [viewingProduct, setViewingProduct] = useState<Product | null>(null);
  const [adminOpen, setAdminOpen] = useState(false);
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);
  const { toasts, addToast, removeToast } = useToast();

  // Load from Cloud Sync on mount
  useEffect(() => {
    async function fetchCloudData() {
      try {
        const cloudProducts = await CloudSync.getProducts();
        if (cloudProducts && cloudProducts.length > 0) {
          setProducts(cloudProducts);
        } else {
          const localProd = localStorage.getItem('glow_home_products_v2');
          if (localProd) setProducts(JSON.parse(localProd));
        }

        const cloudSettings = await CloudSync.getSettings();
        if (cloudSettings) {
          setSettings(cloudSettings);
        } else {
          const localSet = localStorage.getItem('glow_home_settings_v2');
          if (localSet) setSettings(JSON.parse(localSet));
        }
        setIsCloudConnected(true);
      } catch (err) {
        console.warn('Sync fallback active');
      }
    }
    fetchCloudData();
  }, []);

  const handleSaveProducts = async (newProducts: Product[]) => {
    setProducts(newProducts);
    try {
      await CloudSync.saveProducts(newProducts);
      setIsCloudConnected(true);
    } catch (e) {
      console.error('Cloud sync error', e);
    }
  };

  const handleSaveSettings = async (newSettings: StoreSettings) => {
    setSettings(newSettings);
    try {
      await CloudSync.saveSettings(newSettings);
      setIsCloudConnected(true);
    } catch (e) {
      console.error('Settings cloud sync error', e);
    }
  };

  const handleOrder = async (product: Product) => {
    const msg = buildOrderMessage(product, settings);
    await copyToClipboard(msg);
    addToast('success', 'تم نسخ تفاصيل الطلب! جارٍ تحويلك لإنستغرام...');
    setTimeout(() => {
      window.open(settings.instagramUrl, '_blank');
    }, 1200);
  };

  const handleRate = (productId: string, stars: number) => {
    setUserRatings((prev) => ({ ...prev, [productId]: stars }));
    const current = ratings[productId] || { avg: 5, count: 1 };
    const newCount = current.count + 1;
    const newAvg = (current.avg * current.count + stars) / newCount;
    setRatings((prev) => ({ ...prev, [productId]: { avg: newAvg, count: newCount } }));
    addToast('success', 'شكراً لتقييمك للمنتج!');
  };

  const filteredProducts = useMemo(() => {
    return products.filter((p) => {
      const matchesCategory = selectedCategory === 'all' || p.category === selectedCategory;
      const matchesSearch = p.name.toLowerCase().includes(searchQuery.toLowerCase());
      return matchesCategory && matchesSearch;
    });
  }, [products, selectedCategory, searchQuery]);

  return (
    <div className="min-h-screen bg-[#050508] text-zinc-100 font-sans selection:bg-teal-500 selection:text-zinc-950">
      <AuroraBackground />
      <ToastContainer toasts={toasts} onClose={removeToast} />

      <Header
        settings={settings}
        onAdminClick={() => setAdminOpen(true)}
        onMenuToggle={() => setMobileMenuOpen(!mobileMenuOpen)}
        mobileMenuOpen={mobileMenuOpen}
        isCloudConnected={isCloudConnected}
      />

      <Hero
        settings={settings}
        onShopNow={() => {
          const el = document.getElementById('catalog');
          el?.scrollIntoView({ behavior: 'smooth' });
        }}
        productCount={products.length}
      />

      <main id="catalog" className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
        <div className="flex flex-col md:flex-row items-center justify-between gap-4 mb-10">
          <div className="flex items-center gap-2 overflow-x-auto w-full md:w-auto pb-2 md:pb-0 no-scrollbar">
            {getOrderedCategories(settings.categoryOrder).map((cat) => {
              const Icon = cat.icon;
              const active = selectedCategory === cat.id;
              return (
                <button
                  key={cat.id}
                  onClick={() => setSelectedCategory(cat.id)}
                  className={`flex items-center gap-2 px-5 py-3 rounded-2xl font-bold text-sm whitespace-nowrap transition border ${
                    active
                      ? 'bg-teal-500 text-zinc-950 border-teal-400 shadow-lg shadow-teal-950/80'
                      : 'bg-zinc-900/80 text-zinc-400 hover:text-zinc-100 hover:bg-zinc-800 border-zinc-800/80'
                  }`}
                >
                  <Icon size={16} />
                  <span>{cat.label}</span>
                </button>
              );
            })}
          </div>

          <div className="relative w-full md:w-72">
            <Search size={18} className="absolute right-4 top-1/2 -translate-y-1/2 text-zinc-500" />
            <input
              type="text"
              value={searchQuery}
              onChange={(e) => setSearchQuery(e.target.value)}
              placeholder="ابحث عن منتج..."
              className="w-full pl-4 pr-11 py-3 rounded-2xl bg-zinc-900/80 border border-zinc-800 text-zinc-100 placeholder:text-zinc-600 text-sm focus:outline-none focus:border-teal-500"
            />
          </div>
        </div>

        {filteredProducts.length === 0 ? (
          <div className="text-center py-20 bg-zinc-900/40 rounded-3xl border border-zinc-800/80">
            <Package size={48} className="mx-auto text-zinc-700 mb-4" />
            <h3 className="text-xl font-bold text-zinc-200 mb-2">لا توجد منتجات مطابقة</h3>
            <p className="text-zinc-500 text-sm">جرب البحث بكلمات أخرى أو اختر تصنيفاً مختلفاً</p>
          </div>
        ) : (
          <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
            {filteredProducts.map((prod, idx) => (
              <ProductCard
                key={prod.id}
                product={prod}
                onOrder={handleOrder}
                onView={(p) => setViewingProduct(p)}
                index={idx}
              />
            ))}
          </div>
        )}
      </main>

      <footer className="border-t border-zinc-900 py-12 mt-20 bg-zinc-950">
        <div className="max-w-7xl mx-auto px-4 text-center">
          <p className="text-zinc-500 text-sm">
            © {new Date().getFullYear()} {settings.storeName}. جميع الحقوق محفوظة.
          </p>
        </div>
      </footer>

      <ProductDetailModal
        product={viewingProduct}
        settings={settings}
        onClose={() => setViewingProduct(null)}
        onOrder={handleOrder}
        ratings={ratings}
        userRating={viewingProduct ? userRatings[viewingProduct.id] || 0 : 0}
        onRate={handleRate}
      />

      <AdminPanel
        open={adminOpen}
        onClose={() => setAdminOpen(false)}
        products={products}
        onSaveProducts={handleSaveProducts}
        settings={settings}
        onSaveSettings={handleSaveSettings}
        addToast={addToast}
      />
    </div>
  );
}
